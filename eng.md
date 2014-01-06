**A note from the editors:** We are pleased to present you with an excerpt from
[Sass For Web Designers][1] by Dan Cederholm, available now from 
[A Book Apart][2].

I was a reluctant believer in Sass. I write stylesheets by hand! I don’t need
help! And I certainly don’t want to add extra complexity to my workflow. Go away!

That was the thinking anyway. But the reality is that Sass (and other CSS
preprocessors) can be a powerful ally—a tool that any style-crafter can easily 
insert into their daily work. It took me a while to come around, but I’m sure 
glad that I did.

And that’s the reason I wanted to write this little book. To share how I’ve
been able to use Sass to be more efficient, while maintaining the process I’ve 
become comfortable with from writing CSS for the last ten years. I had many 
misconceptions about Sass that prevented me from giving it a go, initially. I 
was worried I’d have to completely alter the way I write and manage stylesheets.
As CSS can be fragile at times, it’s understandable for its authors to be 
somewhat protective about their creation. Can I get an amen?

Ahem.

So, I’m here to show you how Sass doesn’t have to disrupt your process and
workflow, and how it can make your life easier. I’ll demonstrate the various 
aspects of Sass, how to install it, how to use it, and how it’s helped me in my 
own projects. With any luck, I just might make you a believer as well.

## The Sass elevator pitch

Ever needed to change, say, a color in your stylesheet, and found that you had
to find and replace the value multiple times? Don’t you wish CSS allowed you to 
do this?

    
           $brand-color: #fc3;
    a {
    color: $brand-color;
    }
    nav {
             background-color: $brand-color;
    }
    

What if you could change that value in one place and the entire stylesheet
reflected that change? You can with Sass!

Or how about repeated blocks of styles that are used in various locations
throughout the stylesheet?

    
    p {
    margin-bottom: 20px; font-size: 14px; line-height: 1.5;
    }
    footer {
             margin-bottom: 20px;
             font-size: 14px;
             line-height: 1.5;
    }
    

Wouldn’t it be fantastic to roll those shared rules into a reusable block?
Again, defined only once but included wherever you needed them.

    
         @mixin default-type {
         margin-bottom: 20px;
         font-size: 14px;
         line-height: 1.5;
    }
    p {
    @include default-type;
    }
    footer {
         @include default-type;
    }
    

That’s also Sass! And those two extremely simple examples barely scratch the
surface as to how Sass makes authoring stylesheets faster, easier, and more 
flexible. It’s a welcome helper in the world of web design, because anyone that’
s created a website knows
…

## CSS is hard

Let’s face it: learning CSS isn’t easy. Understanding what each property
does, how the cascade works, which browser supports what, the selectors, the 
quirks, and so forth. It’s not easy. Add on top of that the complexity of the 
interfaces we’re building these days, and the maintenance that goes along with 
that and—wait, why are we doing this again? It’s a puzzle, and some of us enjoy 
the eventual completion.

Part of the problem is that CSS wasn’t originally designed to do the things
we do with it today. Sure, progress is moving along at a nice clip thanks to 
rapid browser innovation and implementation of CSS3 and beyond. But we still 
need to rely on techniques that are, for all intents and purposes, hacks. The
`float` property, for example, was designed to simply align an image within a
block of text. That’s it. Yet we’ve had to bend that property to lay out entire 
interfaces.

Our stylesheets are also immensely repetitive. Colors, fonts, oft-used
groupings of properties, etc. The typical CSS file is an extremely linear 
document—the kind of thing that makes an object-oriented programmer want to tear
their hair out. (I’m not an object-oriented programmer, but I have very little 
hair left. Read into that as you may
).

As interfaces and web applications become more robust and complex, we’re
bending the original design of CSS to do things it never dreamed of doing. We’re
crafty like that. Fortunately, browser makers adopt new CSS features far more 
rapidly these days, with more efficient and powerful properties and selectors 
that solve the problems today’s web poses. Features like new layout options in 
CSS3,`border-radius`, `box-shadow`, advanced selectors, transitions, transforms
, animation, and so on. It’s an exciting time. And yet, there’s still a lot 
missing from CSS itself. There are holes to be plugged, and the life of a 
stylesheet author should be a lot easier.

### The DRY principle

If we peer into the world of software engineering (and I much prefer to peer
than hang out and get comfortable there), we can quickly see how organization, 
variables, constants, partials, etc., are an ingrained, crucial way of working 
for folks building complex systems.

You may have heard of the “don’t repeat yourself” (DRY) principle. Coined
and defined by Andy Hunt and Dave Thomas in their book,*The Pragmatic
Programmer* (<http://bkaprt.com/sass/1/>), DRY declares:<figure class="quote
">

> Every piece of knowledge must have a single, unambiguous, authoritative
> representation within a system.
></figure>
The idea is that duplicating code can cause failure and confusion for
developers
(<http://bkaprt.com/sass/2/>). It’s common sense as well: write commonly-
repeated patterns once, and reuse those bits throughout the application. It’s 
more efficient and far easier to maintain code this way.

CSS is anything but DRY. At times, it drips with repeated rules, declarations,
and values. We’re constantly writing the same snippets of code for colors, fonts,
and frequently-used patterns of style throughout our stylesheets. One look 
through a decent-sized CSS file, and a DRY software developer will weep, first 
with bewilderment, then frustration.

“How the !@#$ do you maintain this?!” they’ll ask.

“Have I also told you about IE bugs?” you’ll reply with a bit of self-
loathing.

### So why is CSS so difficult to work with?

We can gather a hint of understanding why CSS has had its syntax limitations
over the years from an essay by CSS co-inventor, Bert Bos
(<http://bkaprt.com/sass/3/>):<figure class="quote">

> CSS stops short of even more powerful features that programmers use in their
> programming languages: macros, variables, symbolic constants, conditionals, 
> expressions over variables, etc. That is because these things give power-users a
> lot of rope, but less experienced users will unwittingly hang themselves; or, 
> more likely, be so scared that they won’t even touch CSS. It’s a balance. And 
> for CSS the balance is different than for some other things.
></figure>
The original architects of CSS were concerned with adoption. They (rightfully)
wanted as many people as possible creating websites. They wanted CSS to be 
powerful enough to style web pages and separate content from presentation, while
being easy to understand and use. I can certainly respect that. At the same time,
we have work to do, and that work is getting more complicated, more nuanced, and
more challenging to maintain and to future-proof.

Fortunately, there are options to help us out here, and one of them is Sass.

## What is Sass?

Sass is a CSS preprocessor—a layer between the stylesheets you author and the
`.css` files you serve to the browser. Sass (short for Syntactically Awesome
Stylesheets) plugs the holes in CSS as a language, allowing you to write DRY 
code that’ll be faster, more efficient, and easier to maintain.

The Sass website (<http://bkaprt.com/sass/4/>) describes itself succinctly:<
figure class="quote
">

> Sass is a meta-language on top of CSS that’s used to describe the style of
> a document cleanly and structurally, with more power than flat CSS allows. Sass 
> both provides a simpler, more elegant syntax for CSS and implements various 
> features that are useful for creating manageable stylesheets.
></figure>
So while normal CSS doesn’t yet allow things like variables, mixins (reusable
blocks of styles), and other goodies, Sass provides a syntax that does all of 
that and more—enabling “super functionality” in addition to your normal CSS. It 
then translates (or compiles) that syntax into regular ol’ CSS files via a 
command-line program or web-framework plugin.

More specifically, Sass is an extension of CSS3, and its SCSS (“Sassy CSS
”) syntax—which we’ll talk about in just a moment—is a superset of CSS3. Meaning,
any valid CSS3 document is a valid SCSS document as well. This is integral to 
Sass being something you can “ease into.” Getting started with Sass syntax is 
painless, and you can use as little or as much as you’d like. Which also means 
converting an existing stylesheet from CSS to SCSS can be done in stages, as you
learn and pick up more of Sass’s functionality.

Later, when you’ve become fluent with Sass (and it won’t take long), it
really does feel like a natural extension of CSS—as if it’s filling holes we all
wish were filled by the CSS spec itself. This is why, once I started using Sass,
I never once thought it was awkward or laborious—it just feels like CSS should 
feel. Once you try it, you’ll likely stick with it permanently.

Furthermore, Sass is helping CSS get better. By fast-tracking certain features
that aren’t currently possible without the help of a preprocessor, it’s giving 
CSS authors real-world implementation and feature experimentation. When and if 
it makes sense, certain Sass functionality could very well inform future CSS 
specifications.

## Sass misconceptions

I mentioned earlier that I was reluctant to try Sass. This was partly due to a
lot of misconceptions I had prior to using it. Do I need to know Ruby or 
advanced command-line shenanigans? Will I need to completely change the way I’ve
been writing stylesheets? Will the CSS it outputs be bloated and unreadable?

Thankfully, the answer is “nope” for each of those questions, of course—
but I do hear them pop up whenever someone mentions Sass on various internet 
channels. Let’s clear up a few things.

### I’m afraid of the command line!

I am by no means a command-line expert, but I’ve learned a bit here and there
over the years—just enough to get me into trouble. I’m not afraid to traverse 
the file system with it or use Git commands, etc.

That said, I sympathize with designers and front-end developers who don’t
want to go there. There’s a command-line phobia that exists among some folks. 
For Sass, there’s very little command-line action required—in fact, a single 
command is all you need to grasp. Additionally, there are apps and web 
frameworks that will obviate the need for the command line. (I’ll be introducing
those in the next chapter
).

So, if you’re a command-line avoider, don’t let that stop you from trying
Sass!

### I don’t want to change the way I write CSS!

This was the misconception that I suffered from. I’m particular about the way
my stylesheets are set up and organized. There’s a certain amount of craft that 
goes into the document. But remember, since the SCSS syntax is a superset of 
CSS3, you don’t have to change anything about the way you write CSS. Commenting,
indenting, or not indenting, all your formatting preferences can remain the same
when working in`.scss` files. Once I realized this, I could dive in without
fear.

### I don’t want Sass to change the way I design!

On the flip side, Sass won’t solve all of your problems or cure your bad
habits. Inefficient, bloated stylesheets can be just as inefficient and bloated 
when using Sass. Good organization and smart thinking still apply here. In fact,
there are instances where Sass can magnify bad practices, and we’ll go into that
a bit as well. But when used properly and intelligently, Sass can be such a 
massive assist in creating websites.

Okay. Now that we have the particulars out of the way, let’s start having
some fun. I think you’ll be amazed at what Sass can do. In the next chapter, we’
ll set up our workflow—how Sass can fit into your process and how easy it is to 
use the command-line or apps. Let’s get Sassing, people.

 [1]: http://www.abookapart.com/products/sass-for-web-designers
 [2]: http://www.abookapart.com/