This project is divided into two major things: the inner workings, and everything else that uses these workings.

The everything else is more or less my own way to allow collaboration and sales of goods online, and allows me to organize my thoughts in a way I find important to me.

Having an inner core and outer layers is good for me to write because of how my mind works, I concentrate on the very detailed, to the broad picture, back and forth, a lot.
Designing this helps me concentrate on one or the other as I need to. The inner core is very innery, if that is a word. The outer core is very outery

If I had to define the inner core in two words it would be: super tagger.
When you tag something, it adds some information to what it is. The inner core tags and tags and tags, then tags the tags, then spins it all about.
I know that is not very helpful but there is madness in the method, so let me explain.

We need to have some red marbles. Never mind what for. We need some to carry in a bag. Later on we are going to do stuff with the red marbles in our bag, and give some to our friend.

So, we need a way to manufacture the red marbles. Its not like I am going to build each on their own. We need sort of a template for a red marble.

How do we build it? Well, we start with a plain transparent marble. Later on we will have all sorts of marbles. But they are now all plain glass marbles that look the same if we make them.
These marbles are called tokens.

We do not really make marbles here in this project, its not that sort of thing. But in this example, every single token is a marble. 

If we want a red marble, then we will put a tag on it that says red. We call this red tag an attribute. We call the template a token-type because it describes a type of token.
First we need an attribute with the name red, and the value of the rbg red OxF00 (css color for red).

First we make the red attribute by itself, with a default value of 0xF00. This red attribute has its own lifecycle. It can be used in many marble types.
Then we make a token-type that has one red attribute. Then we call an api to make a red marble.

The token type is also its own thing. It has a life of its own, and does not go away as soon as I make the marbles. It sticks around. Later on I will have more uses for it.

Now that we have the attribute, and the token type, we can make as many red marbles as we want.
Later, there will be restrictions to some other marbles we might like to make, particularly when we use someone's else's pattern scheme we like. 

Because I am going to make more marbles. I will need a bag to carry them in. This bag is called a set, and my bag of marbles is called a set of marbles.

Now we make some more marbles and put them in a set of ten red marbles.

In real life, each marble can be a bit different, if not made in a big factory that prides itself in making exact copies that look that same. 
We are going to pretend that are marbles are locally made, and have some subtle differences from time to time. 
So, here, in our example, we want two of the marbles to be shinier, and one to be a deeper red color.

But at the same time, we still want all the marbles in this bag to have the same attributes. Later on we will have bags that have different marbles.
But now, lets forget about the first bag and make another.

I will make another attribute with the name of shiny and the default value of 5, because on a scale of 1 - 10 5 is average. 
Then, I am going to edit my token type.. oh, I cannot because it's being used in my basic red marbles.
Oh well, I will make a new token type that inherits from the red marbles, and it has its own shiny attribute too.
Now I have a shiny red marble token-type that makes average shiny marbles, because each marble made will have a shiny value of 5. And I make a new set of 10 of these.

To make two of the marbles shinier, I increase the shiny value directly on two of them, because I can. Their shiny value is now 8.
To make one of the marbles darker red, I change one marble's red attribute to be darker : 0xA00.