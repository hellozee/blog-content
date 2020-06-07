+++
title = "Done with boost"
date = 2019-06-15T00:16:56+05:30
tags = ["krita","gsoc","open-source","kde","boost","cpp"]
categories = ["krita"]

+++

This would start with a quote:

> Documentation is like sex: when it is good, it is very, very good; and when it is bad, it is better than nothing.
>
> `- Dick Brandon (Honestly, I have no idea who this is)` 

One of the so called pillar of the `c++` world, `boost`, sucks a lot when it comes to documentation, I wouldn't have to write more than one blog post if they had their documentation in place. It has been almost a month that I have started working on the Magnetic Lasso and I wasted most of the time fighting with `boost` instead of working on my algorithm. Okay, fine I am getting paid for it, I shouldn't complain.

Now the good sides, learnt a lot about how to read template errors and also how to reduce all the gibberish which the compilers throw when they get one, so the key take ways from the fight would be,

- learnt about `BOOST_CONCEPT_ASSERT`, this thing deserves a separate blog post, such a cool thing it is
- `clang` provides much better error messages than `gcc`, switching compilers can help sometime
- C++ traits, another sweet thing which go hand in hand with concepts

As I was discussing in [this](https://hellozee.github.io/boost_astar/) post, that `boost::astar_search` requires a bunch of maps, turns out, I was underestimating their number, let me list them one by one here, 

- Predecessor Map
- Distance Map
- Rank Map
- Vertex Index Map
- Weight Map
- Color Map
- Some more, but I won't be talking about them

Shit, I feel like an atlas now, too many maps. Anyway, thankfully, I got around most of them using `std::map` but some needed a little bit of special attention, because of you know, `traits`.

### Predecessor Map

```c++
struct PredecessorMap{
    PredecessorMap()
    { }

    PredecessorMap(PredecessorMap const& that):
    m_map(that.m_map)
    { }

    typedef VertexDescriptor key_type;
    typedef VertexDescriptor value_type;
    typedef VertexDescriptor & reference_type;
    typedef boost::read_write_property_map_tag category;
```

See those `typedef`'s these are the respective traits, honestly it feels like magic on how they work mostly, but once you get their point, it feels natural, embedding instead of inheriting, though I may be wrong as this things are still fairly new to me.

```c++
    VertexDescriptor &operator[](VertexDescriptor v){
        return m_map[v];
    }

    std::map<VertexDescriptor, VertexDescriptor> m_map;
};
```

Wrapping up square brackets operator to play nice with `std::map`. I wish if C++ had features like Go has when it comes to embedding types, or probably it has and I have never looked for one.

```c++
VertexDescriptor get(PredecessorMap const &m, VertexDescriptor v){
    typename std::map<VertexDescriptor, VertexDescriptor>::const_iterator found = m.m_map.find(v);
    return found != m.m_map.end() ? found->second : v;
}

void put(PredecessorMap &m, VertexDescriptor key, VertexDescriptor value){
    m.m_map[key] = value;
}
```

Why did I overload the square brackets? I don't know, typical stuff, when you just try adapting an example someone wrote for their own code, though having an extra function doesn't hurt, so I would let it be like these for the moment.

### Distance Map

This one was more forgiving,

```c++
struct DistanceMap {
    typedef VertexDescriptor key_type;
    typedef double data_type;
    typedef std::pair<key_type, data_type> value_type;

    DistanceMap(double const& dval)
            : m_default(dval)
    { }

    data_type &operator[](key_type const& k) {
        if (m.find(k) == m.end())
            m[k] = m_default;
        return m[k];
    }

private:
    std::map<key_type, data_type> m;
    data_type const m_default;
};
```

3 traits and again wrapping up `std::map` .

### Weight Map

```c++
struct WeightMap{
    typedef std::pair<VertexDescriptor, VertexDescriptor> key_type;
    typedef double data_type;
    typedef std::pair<key_type, data_type> value_type;

    WeightMap() { }

    WeightMap(KisMagneticGraph g):
        m_graph(g)
    { }

    data_type& operator[](key_type const& k) {
        if (m_map.find(k) == m_map.end()) {
            double edge_gradient = m_graph.getIntensity((k.first)) + m_graph.getIntensity((k.second))/2;
            m_map[k] = EuclideanDistance(k.first, k.second) * (edge_gradient + 1);
        }
        return m_map[k];
    }

private:
    std::map<key_type, data_type> m_map;
    KisMagneticGraph m_graph;
};
```

I wish I just could have used a single generic map class for both Distance and Weight Maps but I just can't due that pesky weight function, which takes the euclidean distance as well the edge gradient.

For the rest of the maps, it was just using the regular `std::map` with proper types and leave the grunt work of adding traits and functions to boost and at the end the function call looked like this,

```c++
boost::astar_search_no_init(
     g, start, heuristic
    ,boost::visitor(AStarGoalVisitor(goal))
    .distance_map(boost::associative_property_map<DistanceMap>(dmap))
    .predecessor_map(boost::ref(pmap))
    .weight_map(boost::associative_property_map<WeightMap>(wmap))
    .vertex_index_map(boost::associative_property_map<std::map<VertexDescriptor,unsigned>>(imap))
    .rank_map(boost::associative_property_map<std::map<VertexDescriptor, unsigned>>(rmap))
    .color_map(boost::associative_property_map<std::map<VertexDescriptor, boost::default_color_type>>(cmap))
    .distance_combine(std::plus<double>())
    .distance_compare(std::less<double>())
);
```

Man, thats a spaghetti but can't help, it is `boost` we are talking about, fully generic stuff.

I really like some aspects of `boost`, for example embedding instead of inheritance, it is similar to how like that no exception thing in Qt. This things do help a lot in writing more maintainable and legible code.

All the commits along with the description can be found [here](https://phabricator.kde.org/T10894).

And again lets hope by the time I am writing the next post, I am done with algorithm, cause the first evaluation is also approaching pretty fast. After all then you get to brag about that you have at least earned something, thanks Google Summer of Code, `:wq` for now.