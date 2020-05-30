---
layout: post
title: Depth vs. Breadth-first Learning
---
[]: # (Written on 2017-06-02)
![](/images/depth-breadth-learning/learn-benches.jpg)

What if I told you that the foundations of learning structure propagated in the western education system was fundamentally flawed? That there is a better way to learn than how you’ve been taught to learn your entire life? It may come as a bit of a shock, but I strongly believe this to be the case. **In the modern education system, we utilize a depth-first learning structure**, in which we drill very deeply into one subject before moving on to the next, *without any initial explanation as to why we’re learning what we’re learning or how the entire puzzle fits together*. This leads to over-compartmentalization and does not communicate the motivation behind learning the concept in the first place. Instead, I recommend a different approach, namely a **breadth-first learning structure** in which progressively more and more detailed overviews are given, **covering all topics within a field concurrently** to better understand the overall picture and how what you are learning in one subfield applies to the others. I further extend this to the learning of any topic outside of the classroom and will demonstrate with examples how this can be applied.

So now I’ve given an overview of what I’m wanting to teach. You hopefully now understand the overarching picture and how the pieces fit before delving into the nitty gritty. Because so much of this discussion relies on at least a basic understanding of depth and breadth-first search algorithms, I will go into detail presently. 

## Depth and Breadth-first search: explained
In computer science, there are a variety of different “search algorithms” that are used for information traversal. Depth and breadth-first search are two of the most well-known and having a basic understanding of it will help in understanding my repositioning of learning structures later. First, a practical example.

Say you’re driving from Los Angeles to New York City. First of all, what on earth are you thinking? That’s going to be one hell of a long drive. But anyways, you’re at least interested in minimizing your drive-time, so you put your destination into Google Maps (because I know you’re not one of those people using Apple Maps) and it spits out a few different routes.  How did it find those routes? Did it go all the way down each potential path, one at a time, and compare each path to every other? Or maybe it went 50 miles down each path, evaluated the path with the shortest travel time, and then went another 50 miles through all of the shortest paths. Of course, Google Maps is far more sophisticated than either of these in reality, but if it wanted to be less efficient, it *could*. So now that there is some context, let’s jump into depth-first, first.

### Depth-first Search
Depth-first search takes a search-tree and explores each node to maximum depth. If this sounds a bit abstract, that’s okay–pictures make everything easier!

![](/images/depth-breadth-learning/depth-graph.png)

Starting from the top, “Current State” is a generic term which in the case of our example signifies Los Angeles. This points to three different nodes: n1, n10 and n16. These could represent, say, Las Vegas, Phoenix and Albuquerque on our way to NYC. Branching from these are various different paths with all nodes on the bottom layer representing NYC. **I’ve highlighted in blue here the first full path that this search algorithm would pursue**. You can see that when it first starts investigating node n1, the algorithm fully commits and searches through all sub-nodes of its sub-nodes and so on. I have numbered here the exact path that the algorithm would search through.

### Breadth-first Search
Breadth-first search is related, but takes a much different approach.

![](/images/depth-breadth-learning/breadth-graph.png)

Again, the nodes in the first layer down from the Current State represent the first intermediate routes: Las Vegas, Phoenix and Albuquerque. It searches layer by layer instead of all the way though one node at a time. This is actually an oversimplification as none of the nodes or edges have weights. In our example, this means there is no indication of distance, which of course is not how the real world works. Instead, this model assumes all edges are of the same length. In reality, the algorithm would explore what is, at that time, the shortest distance. This level of detail is not necessary for furthering our discussion here, but for more information, the [problem-solving section of Norvig and Thrun’s AI Udacity course](https://classroom.udacity.com/courses/cs271) does a great job of explaining the algorithm.

## The Modern Education System
So now that we’ve covered these systems, let’s dive into how they relate to the modern education system. For the purposes of this discussion, I will be talking in terms of high school education, but these principles apply to all levels of education. As it stands, curricula focus on one sub-field per year. Let’s take Science as an example. My high school curriculum looked like this:

+ 9th Grade: Biology
+ 10th Grade: Geology
+ 11th Grade: Chemistry
+ 12th Grade: Physics

Your’s likely looked similar. Notice that each sub-field is completely compartmentalized. We learn biology without talking about how it relates to chemistry, physics, or any other subfield. Same goes for each other subject.

Even within the compartmentalized system we currently have, we oftentimes dive straight into learning something without ever explaining how it fits into the larger picture. There seems to be this **idea that the minutia has to be fully explained before ever putting the knowledge in context along the way**. Take for example the way I was taught computer networking. The course started out talking about electrical signals, how different amplitudes and frequencies can be used to represent different combinations of 1’s and 0’s. We then discussed wire types, transportation modes, modulation and multiplexing, and only THEN are packets even mentioned. Move on to different topologies, LANs, WANs, etc. All this time and IP hasn’t even been mentioned, let alone any of the delivery methods like TCP or UDP. Eventually it was all covered, **but without any context as to how each constituent part fit into the overall picture** until each niche was fully explored.

This makes it very different to understand what the motivation is for learning any given detail. One that I remember affecting me quite a lot was high school Trigonometry. I was never told how it was used in physics or engineering, what any of the practical applications were. I was just told “This is a triangle, and these are some ratios that describe them”. Well, who cares about triangles? There are tons of cool shapes! Why are we so fixated on this one single polygon?! For some reason, **modern education doesn’t think we can possibly understand how a given piece fits into the overall picture until we’ve fully and completely studied the niche**.

## An Improved System: Breadth-first Learning
Before talking about how to fix modern education, I’d like to describe **one subject that I think educators are teaching properly: Programming**. If we learned programming the same way the education system teaches other subjects, we’d first delve into NAND gates, HDL, and Assembly. We’d move on to compilers and interpreters. Once all this minutia had been covered without ever mentioning why we were learning any of it, only then would we be introduced to this process called programming.

But that’s not how it’s done, and thankfully so. Instead, we declare “Hello, world!” on day one and the student has already made their first script. We have them use data structures before explaining everything that is happening behind the hood. We don’t bog them down with the particulars of coding efficiency and optimization. Instead, they learn through experience. And I think that people are much the better for it.

So now let’s apply this to a modern subject, say math. Paul Lockhart puts it much more eloquently than I ever could in his seminal diatribe on the matter, [A Mathematician’s Lament](https://www.maa.org/external_archive/devlin/LockhartsLament.pdf), but I will share my own thoughts. As it stands in modern high school education, we learn Algebra, then Geometry, then Trigonometry, and finally some pre-calculus (yeah, yeah, I know what you’re thinking–I took calculus in high school too, calm yourself down). **The thing is, all of these subjects correlate**.

If instead of forcing students to understand the whole of Algebra before moving on to another sub-field, we could take large swaths at a time. It would look something like this:

+ 9th Grade: Beginning HS Math
+ 10th Grade: Intermediate HS Math 1
+ 11th Grade: Intermediate HS Math 2
+ 12th Grade: Advanced HS Math

With each year, all mathematical subjects are covered in **BREADTH**. Starting in 9th grade, students are understanding that algebra, geometry, trig and calculus all interweave and interact with each other in a number of ways which can be applied to the real world in whatever way.  They understand that “this bit of Algebra is applied to that bit of Trig in such and such an instance which we will then use to measure support loads on bridges! Cool, right?! There are a large number other applications, but *that’s why you’re learning this*, it fits into this huge overarching picture.” I think a high schooler would be **much more interested in learning an abstract subject with something a bit more substantive**.

The issue of the level of abstraction taken in math education is another subject in and of itself, but this is a general discussion on learning styles. I hope by now I have adequately communicated how someone may be more likely to pay attention if they first know the motivation behind what they’re learning, viewing each piece in context while they learn it.

## Applying Breadth-first Learning
TODO

So I leave you with that. If you are trying to learn something and you find yourself digging too deep into one niche, try to take a step back and re-evaluate if there are other areas whose depth need further development before moving on.  In the end, I think you will find that this will make the most of your time and leave you with a much better understanding of the subject. Let me know how it goes.
