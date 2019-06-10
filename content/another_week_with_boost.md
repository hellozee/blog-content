+++
title = "Another Week with boost::graph"
date = 2019-06-09T13:29:33+05:30
tags = ["krita","gsoc","open-source","kde","boost","cpp"]
categories = ["krita"]

+++

`<prelude>`

In the previous post, I discussed `boost::astar_search` and ignored the most important part of the whole setup, the graph itself. This I would say is a little harder to comprehend than `boost::astar_search`. And combining that with the horrible documentation boost has, this is a tough gig to crack. Come on boost team, remove those dead links to SGI and replace them with the maintained ones. I guess you people already know HP removed those archives.

Cutting to the point, I should have completed the post way back this Tuesday or Wednesday, but I am yet to even compile the stuff I have written up till now, the compiler complains that the function requires only 1 argument whereas I gave it 11. And if I check the boost source code for the corresponding function call, it apparently requires 11 arguments just like I had given it. Who knows what I did wrong, probably it would take me another week to find out.

`</prelude>`

I would need to derive a graph from an image, from the first look it seems pretty easy, but as I started giving it a thought, things were becoming more and more hazy, one step after another. I had an image which was convolved through a Laplacian of Gaussian matrix, giving me a rough idea of where are edges in the image. Next step converts it to a graph and runs the given start and end points through `astar_search`, boom, we get a nice edge from the start and end points.

Modeling our graph like an [Incidence Graph](https://www.boost.org/doc/libs/1_70_0/libs/graph/doc/IncidenceGraph.html), boost documentation says, it is a refinement over the normal [Graph](https://www.boost.org/doc/libs/1_70_0/libs/graph/doc/Graph.html). And the associated types required are:

- `boost::graph_traits<G>::vertex_descriptor`
- `boost::graph_traits<G>::edge_descriptor`
- `boost::graph_traits<G>::directed_category`
- `boost::graph_traits<G>::edge_parallel_category`
- `boost::graph_traits<G>::traversal_category`

And for Incidence Graph,

- `boost::graph_traits<G>::out_edge_iterator`
- `boost::graph_traits<G>::degree_size_type`

Also, the Incidence Graph requires, the `traversal_category` tag to be convertible to `incidence_graph_tag`.

So first we need a way to describe our vertices, this seems easy, just a couple of coordinates, x and y should be enough to describe a vertex in our graph.

```c++
struct VertexDescriptor {
    long x,y;

    VertexDescriptor(long _x, long _y):
        x(_x), y(_y)
    { }

    bool operator==(const VertexDescriptor &rhs) const {
        return rhs.x == x && rhs.y == y;
    }

    bool operator<(const VertexDescriptor &rhs) const {
        return x < rhs.x || (x == rhs.x && y < rhs.y);
    }
};

typedef VertexDescriptor vertex_descriptor;
```

Edges are just a combination of two vertices right?

```c++
typedef std::pair<vertex_descriptor, vertex_descriptor> edge_descriptor;
```

We want our graph to be bidirectional, so there should be no directions,

```c++
typedef boost::undirected_tag directed_category;
```

Nope, there would be no parallel edges,

```c++
typedef boost::disallow_parallel_edge_tag edge_parallel_category;
```

Normal Incidence Graph, nothing fancy, defaults will be fine, 

```c++
typedef boost::incidence_graph_tag traversal_category;
```

Till now, it looks pretty easy, but now the interesting part, how would we perceive that there is an edge between two pixels? Dmitry says all the pixels should be connected to each other, but I doubt, that would even work properly. Why? If all the pixels are connected to each other, then definitely the start and end points are connected to each other, right? AStar would be looking for the smallest path. Taking the fact that both of them are part of a line in the image (it could be any line), the smallest path would be the edge between them, it won't even matter if they are connected visually or not. But then how would you determine the connections? I don't know, I guess I have to follow Dmitry for now, after all, `boost` is a highly generic library, it won't take a lot of changes to adapt it to a new strategy.

And after a little bit of fiddling here and there, I figured out the `out_edge_iterator`  thing, 

```c++
struct neighbour_iterator : public boost::iterator_facade<neighbour_iterator,
                                                             edge_descriptor,
                                                boost::forward_traversal_tag,
                                                             edge_descriptor>
{
    neighbour_iterator(vertex_descriptor v, KisMagneticGraph g):
        graph(g), currentPoint(v)
    {
        nextPoint = vertex_descriptor(g.topLeft.x(), g.topLeft.y());
        if(nextPoint == currentPoint){
            operator++();
        }
    }

    edge_descriptor
    operator*() const {
        edge_descriptor const result = std::make_pair(currentPoint,nextPoint);
        return result;
    }

    void operator++() {
        if(nextPoint == graph.bottomRight)
            return; // we are done, no more points

        if(nextPoint.x == graph.bottomRight.x()) // end of a row move to next column
            nextPoint = vertex_descriptor(graph.topLeft.x(), nextPoint.y++);
        else
            nextPoint.x++;
    }

    bool operator==(neighbour_iterator const& that) const {
        return currentPoint == that.currentPoint && nextPoint == that.nextPoint;
    }

    bool equal(neighbour_iterator const& that) const {
        return operator==(that);
    }

    void increment() {
        operator++();
    }

private:
    KisMagneticGraph graph;
    vertex_descriptor currentPoint, nextPoint;
};

typedef neighbour_iterator out_edge_iterator;
```

And talking about the degree size type, it would be an unsigned integer, so here it is,

```c++
typedef unsigned long degree_size_type;
```

That would mean, I am done with modeling the graph, but not yet with `boost::astar_search`, which I am still stuck with, hopefully, by the time I have to write another post, I will be done with it too. And yes I am yet to push the code to the repository, cause it doesn't compile yet. So `:wq` for now.