+++
title = "Duck typing"
date = 2019-09-14T15:20:04+05:30
tags = ["types", "languages", "c++", "concepts", "templates"]
categories = ["languages"]

+++

> **Definition**: **Duck typing** in computer programming is an application of the [duck test](https://en.wikipedia.org/wiki/Duck_test)—"If it walks like a duck and it quacks like a duck, then it must be a duck"—to determine if an [object](https://en.wikipedia.org/wiki/Object_(computer_science)) can be used for a particular purpose.
>
> `- Dr. WikiPedia`

Seems simple, can be complicated. Why all of a sudden, I am writing about this? As most of you would know, I mostly write and rant about `C++`, `C++11` introduced a magic keyword called `auto` for automatically inferring data types. And was having a *discussion* whether it should be used or not. While the other person was aggressively promoting the usage of auto,  I was more into using it only when I absolutely required. The sole reason I hate most scripting languages is their dynamic typing. 

Coming back to `auto`, I recalled one situation which made me regret for using it.

```C++
auto size_qvector = qvector_object.size(); // returns an int
auto size_vector = std_vector_object.size(); // returns an unsigned long
```

`qvector_object` is an object of `QVector` class, which `Qt` provides, `std_vector_object` is an object of `std::vector` available in the standard library. Both of them function almost in the same way and both of them have a size method to get the current size of the vector. But the `QVector` one returns an `int` while the `std::vector` one returns an `unsigned long`. To be honest it doesn't look that harmful in the first sight. But the moment you start decrementing both, the story changes. Well, I was kind of responsible for the situation too, cause I used `-1` to show the object hasn't been used at all and when you give a negative value to an unsigned variable, we all know what kind of ugly stuff can happen. On top that, this thing can go entirely unnoticed while writing the code, if not properly tested can also land into production some day.

Okay now, more about duck typing and obviously everything is going to be in `C++`. Lets try a traditional example,

```c++
#include <iostream>                                                              
#include <memory>                                                               
                                                                                
struct duck {                                                                   
    virtual void quack() = 0 ;                                                  
};                                                                              
                                                                                
struct random_animal : public duck {                                            
    void quack() {                                                              
        std::cout << "animal quack" << std::endl;                                      
    }                                                                           
};

struct random_bird : public duck {                                            
    void quack() {                                                              
        std::cout << "bird quack" << std::endl;                                      
    }                                                                           
}; 
                                                                                
void make_quack(std::shared_ptr<duck> d){                                       
    d->quack();                                                                 
}                                                                               
                                                                                
int main(){                                                                     
    // one of the cases where it is safe to use auto                               
    auto animal = std::make_shared<random_animal>();
    auto bird = std::make_shared<random_bird>();
    make_quack(animal);        
    make_quack(bird);
}

Output:
animal quack
bird quack
```

If that was a traditional example what would a non traditional example look like? lets see that too,

```C++
#include <iostream>
#include <iomanip>

template<typename Shape>
struct base_shape {
    typedef int perimeter_type;
};
 
struct triangle{
    int _a, _b, _c;
    triangle(int a, int b, int c):
        _a(a), _b(b), _c(c)
    { }
 
    int perimeter(){
        return _a + _b + _c;
    }
};
 
template<>
struct base_shape<triangle>{
    typedef int perimeter_type;
};
 
struct rect{
    int _a, _b;
    rect(int a, int b):
        _a(a), _b(b)
    { }
 
    double perimeter(){
        return 2*(_a + _b);
    }
};
 
template<>
struct base_shape<rect>{
    typedef double perimeter_type;
};
 
template<class Shape>
typename base_shape<Shape>::perimeter_type get_perimeter(Shape s){
    return s.perimeter();
}
 
int main(){
    std::cout << std::fixed << std::setprecision(5);
    triangle t(4,5,6);
    std::cout << get_perimeter(t) << std::endl;
    rect r(5,4);
    std::cout << get_perimeter(r) << std::endl;
    return 0;
}

Output:
15
20.00000
```

In the above case it was more if it has a perimeter, it is a shape instead of if it quacks like a duck it is a duck.

But the most important part is, both of them show the same thing, that is Interface Based Programming, with one showing runtime polymorphism and another compile time polymorphism. The first example is pretty easy to understand and also can be seen in "Introductory C++" courses, the second one is kind of hard to get at the first sight, but it is far more efficient than the first one. The types are decided while the program is compiling in the second example, instead of the runtime which makes compiling take a little bit more time but that is more reliable and faster during runtime.

I am darn sure most of the folks reading this post would be like, but hey, have you ever seen the how the compiler behaves on finding a template error? Yes, a definitely yes, I have wasted not a day but a whole week debugging one of such errors. The errors are pretty disheartening and depressing, it is hard to make sense out of them, even though we can't fully take care of that, we can tackle the situation up to a state where it can be tolerated by using `concepts`. And thankfully I won't go blabbering anymore, cause there are some wonderful blogs for understanding concepts, you can find them [here](https://akrzemi1.wordpress.com/2016/03/21/concepts-without-concepts/) and [here](https://kukuruku.co/post/boost-concepts/).