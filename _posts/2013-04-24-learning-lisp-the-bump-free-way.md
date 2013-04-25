---
layout: post
title: "Learning Lisp The Bump Free Way(take two)"
---

**Since posterous is shutting down and my old blog is soon to disappear, I decided to go through it and see if there is anything in it I would like to republish. Turns out not much is worth saving. My post "Learning lisp: the bump free way" from january 2011 got some circulation, and I thought maybe that one deserves to live on. But then I re-read it and decided to edit it, and rewrite most parts. Hope it's an improvement.**

As a relatively new Common Lisp user, I've compiled a list of notes and tips on learning it. It's a synthesis of my own experience, as well as my observations of the Lisp world. Lisp has a reputation as a hard to learn language, and I believe this is not the case, but there are such things as bumps on the road. Some of them are false beliefs about lisp that might scare people, others are actual nuisances that need to be dealt with, yet others are simply culture shock. Since Lisp is old, it has it's own distinct culture and jargon, and people often get confused or put off by the differences.

### Where to start

Unlike other languages like say python, Lisp doesn’t have one canonical place to "get" Lisp and its docs. New users have questions
like "which compiler should i use?" and "where should I start with learning Lisp?". The answer these people usually get is, start out
with [SBCL](http://sbcl.org) or[CCL(Clozure Common Lisp)](http://ccl.clozure.com/)(I recommend CCL
on Windows and OS X). I've written a short set up guide for both [in my ebook on Lisp web development](http://lispwebtales.ppenev.com/chap07.html#appendix-a-getting-started).
It also covers installing quicklisp, the Lisp package manager used for installing libraries. 

As for learning the language, people who are new to programming in general usually get refered to
[Common Lisp: A gentle introduction to symbolic computation](http://www.cs.cmu.edu/~dst/LispBook/). I also like the simple tutorial
[Lisp In Small Parts](http://lisp.plasticki.com/) originally written for the authors teenage daughter.  If you already have some
programming experience,  [Peter Seibel’s Practical Common Lisp](http://www.gigamonkeys.com/book/)
is the recommended starting point.

In my [ebook](http://lispwebtales.ppenev.com/chap08.html) I've also included some links to [cliki](http://cliki.net), the Common Lisp wiki
which has a ton of information about [getting started](http://www.cliki.net/Getting%20Started), and what
[libraries are recommended](http://www.cliki.net/current%20recommended%20libraries).

I also recommend looking for help on the #lisp and #clnoobs irc channels on [freenode](http://freenode.net/). For people interested in
web development, there is also #lispweb, where I hang out.

### The parenthesis

<img src="/parens.png"></img>

The most notorious of all bumps is Lisp's "idiosyncratic" syntax. Dealing with parens is actually very easy, both reading and writing them. But why would you want to? Can't you just have a "normal" syntax? Here is my list of reasons why I prefer lisp syntax to "normal" syntax(In order of importance):

* They are pretty. I Like looking at them, I'm weird like that :)
* Editing becomes easier. Lisp code is composed of delimited expressions. So when you edit Lisp, you're not editing a stream of characters, but a tree of expressions. This has many advantages, like selecting a whole expression is easier, copy/cut and paste are easier, you can navigate the source quicker, instead of moving the cursor character by character, you move it expression by expressions, so to speak.
* Your editor can re-indent your code *for* you. I hate indenting my code, when my computer can do it for me. Why should I waste my time, while my CPU is idling? I shouldn't.
* You get *all* the nice things you might have heard about a thing called *homoiconicity*. Namely, **MARCROOOS** and compile time meta-programming. 

How do we deal with the slight annoyance of the parens? The most important thing is to have your editor count the parens for you. If you press "(", the editor should insert ")". Emacs's paredit mode even deletes the closing paren when you delete the opening one, ensuring that you always have them balanced. Also important is to have your editor highlight the matching delimiters, if you put your cursor on the opening one, it highlights the closing one. 

Another way to see if you have them at a wrong place is to get an editor that knows how to indent your Lisp code based on the parens, if you auto-indent a block of Lisp code, and it seems badly indented, it's a good sign your parens are misplaced. As for reading code, you have to learn to rely more on the indentation, like you would in python, than the parens to tell the structure of your code. If the parens are distracting you, set your editor syntax highlighting color for them to a light grey, so that they are barely visible. I personally don't like that, but many people report it makes it easier for them to read lisp code. Try this stuff out.

### Dealing with misinformation

Unfortunately the reality of our industry is that it’s driven more by folklore and mythology than by science, which is why every lisp guide has to repeat the same things over and over again in order to overcome peoples preconceptions of what Lisp is. So repeat after me:

* Lisp is compiled, not interpreted(but often you have an interpreter as an option too). In fact, two of the most popular implementations CCL and SBCL both compile to very efficient machine code, makeing lisp one of the fastest languages out there, certainly one of the fastest dynamic languages.
* It’s not just for AI. People have used it for many other things, even though it was originally developed and heavily used in AI. In fact I fail to find a domain that doesn't have an example of lisp usage in it, however humble. 
* It has data structures other than lists. In fact, other than the built in ones, like arrays and hash tables, there are libraries for many more, including libraries for persistent data structures, you may have heard of them if you've done any functional programming.
* It has ‘for’ loops(and any other loops you might desire, or not), not just recursion. The Lisp *loop* macro is actually a mini-algol like language built into Lisp. It's very cool(or horrifying if you're a fan of functional programming). 
* It’s a multi-paradigm language, not just functional. Most of my code is a mix between OO and some FP. 
* It has an object system. Actually, it not only has one, it has one of the best. I'll go so far as to say that lisp is one of the best OO languages out there. 
* It has libraries, tools, and IDEs. These points I'll address in a minute.
* The community isn't nearly as blood thirsty as some people might portrait it. (most of the time :)

### Do I have to use Emacs? 

Because GNU Emacs is the most commonly used tool for Lisp development(Emacs+Slime is an extremely powerful IDE), newbies often ask if they *have to* learn it. Although lispers will agree that Emacs gives you the most *complete* Lisp experience and it gives you the most convenience in working with Lisp code, if you aren't already an Emacs user, it can be hard to learn it concurrently with learning Lisp. Some people manage, but there is *no need* to do it. If you are a Vim user, the slimv plugin gives you almost all of the niceness of Slime(the emacs mode for working with Lisp). Both are good choices depending on what editor you use. 

Unfortunately no other free editors or IDE's I know of have sufficiently powerful plugins to make editing lisp as easy and as convenient as slime/slimv. At best they give you an experience similar to something like python or ruby, you get a limited prompt, and you have to manually load and run your code, and you don't get the nice object inspector and debugger of slime. If you use something other than emacs/vim, make sure your editor knows how to indent lisp code, and how to count the parens for you, as we discussed previously. And if you are using SBCL, you will also need to use [lineedit](http://common-lisp.net/project/linedit/) to give you a nicer REPL in the console. This gives you about the level of interactivity as using any plain scripting language, but this is pretty sub-optimal from the point of view of an experienced lisper, so consider investing time after learning the basics of Lisp into learning either Emacs or Vim. 

### Lisp is old, and smells like it

Lisp is 50+ years old, the Common Lisp ANSI standard was published in 1994, and the language hasn’t changed since then. Python or ruby people who are used to their language having a new version out every other week might feel a bit shocked by this. Common Lisp certainly has a retro feel to it, and that might be confusing to new people. Why use a language that hasn't changed in 19 years and probably won't change anytime soon either? That sounds like a sure way for your language to die because it can't evolve with the rest of the world.

The good news is that the people who worked on standardizing Lisp knew what they were doing and designed a language that has little trouble adapting to new challenges even though the core doesn't change for decades. Once you get used to the slight annoyence of having the computer talk back at you in *ALL CAPS*, you'll pretty much not think of this as a drawback, but as an advantage. If your code uses only the functions and macros defined in the COMMON-LISP package(packages are like a namespaces in Lisp), your code will NEVER bitrot. 

Yes, Lisp is getting a bit dusty in certain places, some design decisions were made before we knew that EVERY computer on the planet would run a Unix like system, or something sufficiently similar.

But almost all of the problems of Lisp's core design can be solved by libraries. If there is a core design flaw in python, you can't just write a library and have it go away, you have to wait for Guido to recognize it as a flaw(he may disagree) and then the community must find a good solution and release a new version of the language, etc. Since in Lisp, many such flaws can be fixed by libraries, the fact that it doesn't change is irrelevant. The core doesn't change, the extended ecosystem does, and with it, the way the language is used. I find this arrangement to be greatly beneficial to Lisp. 

### I heard lisp doesn't have any libraries

You heard wrong, but I won't deny there aren't enough lispers to maintain a giant ecosystem like the JVM or Python. But we do have a nice small and cozy one, and for everything else, we call out to C libraries for help, not to mention that the [ABCL](http://common-lisp.net/project/armedbear/) compiler has access to anything that runs on the JVM.

Certain domains are very well off, with libraries and tools in sufficient number, quality and a good amount of documentation/tests. Others aren't as maintained, and you'll need to deal with no documentation/tests or abandon-ware. 

Since often times Lisp libraries don't need to change after a certain level of functionality is implemented, you may think that a library is abandoned, when in fact the author simply hasn't found any bugs in it in years, and doesn't need any new features. In lisp, this is ofthen the case and you shouldn't be scared of lines like "last updated: 2009", it might still serve your needs perfectly. 

On the question of documentation, Lisp libraries often have just a simple README, and a few examples, so you may find yourself reading source code at times. Sometimes the documentation is out of date, which I believe is worse than no documentation. Sometimes, the docs are in Russian/Japanese/Whatever. These are all true of every language ecosystem, but like I said, Lisps is a small and cozy one, they become much more visible. Don't panic! This doesn't stop lispers from producing awesome software, it just slows them down a bit from time to time. Pretty much all the important kinds of libraries out there are documented and of high quality. These problems come out in niches with very few interested hackers anyway. 

Not to mention that the situation has been improving in the last few years as new people come along and help out by writing libraries and tutorials, editing [cliki](http://cliki.net) and blogging more. You can help out too! 

Free software is about scratching your own itch, and helping others. If you go on Hacker News and complain about the "lack of lisp libraries", no lisper will care. Or attitude is: You want to help out, great, otherwise, we don't want to hear it. After all, you get what's already there, thousands of dollars worth of software *for free*. A commercial Lisp compiler costs a lot of money, you get several high-quality ones at no cost, and you get all of the source too. It is the same for any community, but lisp and similar sized ones are especially non-sensitive to such complaints. In bigger communities, complaining about X or Y online, might prompt somebody to try and solve it(although it is still a waste of time and annoying), but in Lisp Land, nobody will hold your hand. All of these libraries that you use for free in any language were written by somebody. In lisp, sometimes that somebody is you! Embrace that, and Lisp will make you very happy!!!

### Conclusion

So in order to get the most out of the lisp experience, I have to learn a new way of reading and writing source, using a weird 35 year old editor, use a non-popular language that hasn't changed substantially in 20 years and only has a bare minimum of libraries and documentation to qualify as alive, and I'll likely have to write a lot of common things myself, or at the very least decipher somebody else's code and document it. Not to mention I'll have to explain all of this misinformation people seem to like to spread every time I tell someone I'm using this language. 

When I put it like that, it proves that I suck at marketing. Well, in this post I just wrote about the bad stuff I've encountered and seen others encounter, and wrote about it, so the conclusion I wrote above is one based on a single angle of a side, of a facade, of just one dimension of the richness of lisp culture. So don't think of it as being that bad. This post is about dealing with the little bad there is while *learning*. The good, well, there is way too much praise for Lisp out in the internet for me to care about writing more, but I can say safely that I enjoy working with this language and I love what it has thought me, and I especially enjoy helping others learn it. If this post hasn't scared you away from Lisp, welcome aboard! Hacks and Glory await you!  