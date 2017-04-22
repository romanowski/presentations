# Zinc (sbt) friendly code.

In April I gave a [presentation (50 shades of scala compiler)](TODO) on ScalaUA confrence.  In abstract I promised to give some hits how to write code to be friendly for given compilers. Since it was only only 40 minuets and scala compilers have many, many shades (I almost forgot about dotty!) hints didn't fit into the slides.

I don't like false promises so you can find first batch of hints (related to incremental compiler) below.  

## TL;DR;

If tools and its internals are boring her is condensed list of my advices. All points are explain below.
 
 1. Put at no more theb one class/trait and its companion object in one source file. [More](#less-is-more)
 2. Make you packages small (5-7 sources at most) [More](#wildards)
 3. Add explicit return type for all your public (non-private) methods so they are not changed where is no such need. [More](#types-we-need-more-types)
 3. Make sure that your code is and will be free of unused imports. [More](#unused-ones)
 4. Don't use wildcard imports from packages that often change. Use wildcards only if you must [More](#wildards)
 5. Don't mix implicits and regural public methods in one class. [More](#implicits)
 6. Macros are zinc-killers. Keep them separated and try not to recompile them too often [More](#macros)
 
 
## Don't use names if you don't need them

Zinc (by default from sbt 0.13 version) use name hashing algorithm. In means that relations between source files are based on used names. If `Bar.scala` depend name `foo` from `Foo.scala` and changing `bar()` method in `Foo.scala` will not recompile `Bar.scala`.

This is makes zinc much faster in terms of files recompiled for given change (less is recompiled so compilation is faster) but it will also introduce problems, more below.

Generally next sections are focused on reducing amout of used names to speed up incremental compilations.  

## Less is more. 

Less classes/traits/objects per source file means more times saved. Scalac cannot compile nothing less then a whole source so even if zinc knows that only one-line object needs to be recompiled it has to compile wholes source (and all implicits macros and other nasty stuff).
The soultion is as simple as possible - split your sources! If incremental compilation is not enogh to convince you it should also helps with compilation time or even result in less conflicts during merges.

## Types, we need more types!

// TODO add sth smart about return types!

If you don't provide explicit type scalc will compute one for you. It wil be as presice as possible. Developers love that and later on complain that compilation (even incremental ones) are long? What is the problem with method without explicit type? That it changes. Even without us wanted to changed it. Need an exampe? //TODO Seq and group by example. You may say that as long as your code compiles all is fine. I agree if you don't care for compilation times. Every time type is changed all usages need to be recompiled (and with inremental compiler heuristic even more).

In short words, add return types to all public (or even all non-private) methods.   

## Imports, wildcards and other nastiness.

Most of us don't care about imports. We only need them for code to compile. Even Intellij collapse imports by default:

//TODO pic of import.

Let me show that if you care about your build performance (leaving maintenance conserns for another blog post) correct handling of imports is crucial.

### Unused ones

You may reason that unused imports affects scalc performance (e.g. more implicits to check). Regardless compilation benefits it really affects incremental compilation performance. Even if given import is not used at this moment once changed (the thing behind import, e.g. object) may affect current file. That is why zinc needs to keep relation between sources in such cases. Why is that? It can introduce e.g. new implicit that should be use (or ends up with compilation error). Need and exmaple? See [bug in zinc](TODO) I discovered when writing this blog post.
 
 
 Luckily, removing unused imports is quite easy. The simplest solution is to add `-Ywarn-unused-import` flag to the compier and `-Yfatal-warnings` on PR validation builds. With this you will get notified for every build that you have unused imports and those warnings become error on CI forcing you to clean them up berfore PR is merged. Why not set `-Yfatal-warnings` for all builds? Being forced to comment out imports when you just want check if using `Vector` will make your code faster is really annoying in thelong term.
 
 ### Wildards

As a tooling developer I want to say `don't use them at all!`. I can't (and don't want to) since most of fantastic scala libs start with `import fantastic.lib._`. 

Why wildcard imports are so hard for incremental compiler? Fist step to understand evilness is to try simple test. Replace any of wildcard import with all member of that package and compile it with '-Ywarn-unused-import'. I wish there is a compiler flag that will tell you how much import from given package is used :simle:. 

But this is only the tip of iceberg. With wildcard import incremental copiler needs to be ahead of time one. Why?
Since you not only import all names that exists at the moment of compilation but you also import all that will exisits in future in that package. For incremental compiler old python joke `import jetboard from the.future` has new, bitter taste.

What can I do then? There is no silver bullet for this problem but I can give you some advices:

1. Make you packages (or generally import scope) small. If your package has 5 sources instead of 20 it will make your code much, much easier to learn.
2. Make more use of `private` or `private[your_package]` keywords. I really wish everything is scala is private by default :smile:.
3. Use wildcard imports only from libraries (or pices of code that is changed rarely). Wildcards are dengerous only when imported things changes.

## Implicits

Implicit are probably the hardest part of Scala from incremental compiler perspective. To support implicits effectively and correctly we would need to add relation to *all potential member* of implicit scope. How much connections is that? Way to much to effectively handle all :smile:.

That is why zinc has to use simpler approach for handling implicits. In short word if you use anything from class `Foo` and *any* implicit name from it is changed then our source is recompiled.

What does it means? If you want smooth and incremental compilation don't mix implicits and normal function in single class. Unless you are fine with tons of sources recompiled for no reason!

## Macros

The only way how macros can be supported in incremental compiler is naive brute-force: if macro is recompiled then later on recompile all places where macro is used. It can mean that macros are responsible for the some of the longest incremental compilations. How can we live with that? Either take incremental compilation of macros in you own hands and turn TODO macro flag off or try to remove all cases when macros is recompiled. How to do so?
First of all pull macros to dedicated files, remove any non-macro methods from that files and clean imports. Generaly reduce things imported and used in sources conatining macros.

