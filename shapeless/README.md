# shapeless: generic programming for Scala

**shapeless** is a type class and dependent type based generic programming library for Scala. It had its origins in
several talks by Miles Sabin ([@milessabin][milessabin]), given over the course of 2011, on implementing [scrap your
boilerplate][syb] and [higher rank polymorphism][higherrank] in Scala. Since then it has evolved from being a resolutely
experimental project into library which, while still testing the limits of what's possible in Scala, is being used
widely in production systems wherever there are arities to be abstracted over and boilerplate to be scrapped.

[![Build Status](https://api.travis-ci.org/milessabin/shapeless.png?branch=master)](https://travis-ci.org/milessabin/shapeless)
[![Stories in Ready](https://badge.waffle.io/milessabin/shapeless.png?label=Ready)](https://waffle.io/milessabin/shapeless)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/milessabin/shapeless)
[![Maven Central](https://img.shields.io/maven-central/v/com.chuusai/shapeless_2.11.svg)](https://maven-badges.herokuapp.com/maven-central/com.chuusai/shapeless_2.11)
[![Scala.js](https://www.scala-js.org/assets/badges/scalajs-0.6.8.svg)](https://www.scala-js.org)
[![codecov.io](http://codecov.io/github/milessabin/shapeless/coverage.svg?branch=master)](http://codecov.io/github/milessabin/shapeless?branch=master)

## Projects which use shapeless

There is a wide variety of projects which use shapeless in one way or another ... see the
[incomplete list of projects][built-with-shapeless] for ideas and inspiration. If you are using shapeless and your
project isn't listed yet, please add it.

[built-with-shapeless]: https://github.com/milessabin/shapeless/wiki/Built-with-shapeless

## Finding out more about the project

The [feature overview for shapeless-2.0.0][features200] provides a very incomplete introduction to shapeless.
Additional information can be found in subsequent [release notes][relnotes220]. If you are upgrading from
shapeless-2.0.0 you will find the [migration guide][migration210] useful. We're not satisfied with the current state
of the documentation and would love help in improving it. You can find an excellent guide to Shapeless here:
[The Type Astronaut's Guide to Shapeless](https://github.com/underscoreio/shapeless-guide).

shapeless is part of the [Typelevel][typelevel] family of projects. It is an Open Source project under the Apache
License v2, hosted on [github][source]. Binary artefacts are published to the
[Sonatype OSS Repository Hosting service][sonatype] and synced to Maven Central.

Most discussion of shapeless and generic programming in Scala happens on the shapeless [Gitter channel][gitter]. There
is also a [mailing list][group] and [IRC channel][irc], but these are largely dormant now that most activity has moved
to Gitter. Questions about shapeless are often asked and answered under the [shapeless tag on StackOverflow][so]. Some
articles on the implementation techniques can be found on [Miles's blog][blog], and Olivera, Moors and Odersky, [Type
Classes as Object and Implicits][tcoi] is useful background material.

[features200]: https://github.com/milessabin/shapeless/wiki/Feature-overview:-shapeless-2.0.0
[relnotes]: https://github.com/milessabin/shapeless/wiki/Release-notes:-shapeless-2.0.0
[relnotes220]: https://github.com/milessabin/shapeless/wiki/Release-notes:-shapeless-2.2.0
[migration]: https://github.com/milessabin/shapeless/wiki/Migration-guide:-shapeless-1.2.4-to-2.0.0
[migration210]: https://github.com/milessabin/shapeless/wiki/Migration-guide:-shapeless-2.0.0-to-2.1.0
[milessabin]: https://twitter.com/milessabin
[syb]: http://research.microsoft.com/en-us/um/people/simonpj/papers/hmap/
[higherrank]: http://camlunity.ru/swap/ocaml/Sexy%20Types.pdf
[typelevel]: http://typelevel.org/
[scalaz]: https://github.com/scalaz/scalaz
[spire]: https://github.com/non/spire
[tcoi]: http://ropas.snu.ac.kr/~bruno/papers/TypeClasses.pdf
[source]: https://github.com/milessabin/shapeless
[sonatype]: https://oss.sonatype.org/index.html#nexus-search;quick~shapeless
[wiki]: https://github.com/milessabin/shapeless/wiki
[group]: https://groups.google.com/group/typelevel
[so]: http://stackoverflow.com/questions/tagged/shapeless
[gitter]: https://gitter.im/milessabin/shapeless
[irc]: http://webchat.freenode.net?channels=%23shapeless
[blog]: http://milessabin.com/blog

## Participation

The shapeless project supports the [Typelevel][typelevel] [code of conduct][codeofconduct] and wants all of its
channels (mailing list, Gitter, IRC, github, etc.) to be welcoming environments for everyone.

Whilst shapeless is a somewhat "advanced" Scala library, it is a lot more approachable than many people think.
Contributors are usually available to field questions, give advice and discuss ideas on the [Gitter channel][gitter],
and for people wanting to take their first steps at contributing we have a selection of open issues flagged up as
being [good candidates to take on][lowhangingfruit]. No contribution is too small, and guidance is always available.

[codeofconduct]: http://typelevel.org/conduct.html
[lowhangingfruit]: https://github.com/milessabin/shapeless/issues?q=is%3Aopen+is%3Aissue+label%3A%22Low+hanging+fruit%22

## Using shapeless

Binary release artefacts are published to the [Sonatype OSS Repository Hosting service][sonatype] and synced to Maven
Central. Snapshots of the master branch are built using [Travis CI][ci] and automatically published to the Sonatype
OSS Snapshot repository.

### Try shapeless with an Ammonite instant REPL

The quickest way to get to a REPL prompt with the latest version of shapeless on the class path is to run the
provided ["try shapeless"][try-shapeless] script, which has no dependencies other than an installed JDK. This script
downloads and installs [coursier][coursier] and uses it to fetch the [Ammonite][ammonite] REPL and the latest version
of shapeless. It then drops you immediately into a REPL session,

```text
% curl -s https://raw.githubusercontent.com/milessabin/shapeless/master/scripts/try-shapeless.sh | bash
Loading...
Welcome to the Ammonite Repl 0.7.8
(Scala 2.11.8 Java 1.8.0_102)
@ 23 :: "foo" :: true :: HNil 
res0: Int :: String :: Boolean :: HNil = 23 :: foo :: true :: HNil
@ Bye!
%
```

[try-shapeless]: https://github.com/milessabin/shapeless/blob/master/scripts/try-shapeless.sh
[coursier]: https://github.com/alexarchambault/coursier
[ammonite]: https://github.com/lihaoyi/Ammonite

### shapeless-2.3.2 with SBT

To include the Sonatype repositories in your SBT build you should add,

```scala
resolvers ++= Seq(
  Resolver.sonatypeRepo("releases"),
  Resolver.sonatypeRepo("snapshots")
)
```


[ci]: https://travis-ci.org/milessabin/shapeless


Builds are available for Scala 2.10.x, 2.11.x and for 2.12.x. The main line of development for
shapeless 2.3.2 is Scala 2.12.1. Scala 2.10.x is supported via the macro paradise compiler plugin.

```scala
scalaVersion := "2.12.1"

libraryDependencies ++= Seq(
  "com.chuusai" %% "shapeless" % "2.3.2"
)
```

If you are using Scala 2.10.x, you should also add the macro paradise plugin to your build,

```scala
scalaVersion := "2.10.6"

libraryDependencies ++= Seq(
  "com.chuusai" %% "shapeless" % "2.3.2",
  compilerPlugin("org.scalamacros" % "paradise" % "2.1.0" cross CrossVersion.full)
)
```

### shapeless and Typelevel Scala

[Typelevel Scala][tls] provides a [partial fix for SI-7046][si-7046-pr] which can present obstacles to using
shapeless's `Generic` and `LabelledGeneric` for the sealed trait at the root of an ADT. If it appears that these two
type classes are unable to find (all of) the subclasses of the root trait then please try using Typelevel Scala and
see if it resolves the issue.

To use Typelevel Scala you should,

+ Update your `project/build.properties` to require SBT 0.13.13 or later,

  ```
  sbt.version=0.13.13
  ```

+ Add the following to your `build.sbt` immediately next to where you set `scalaVersion`,

  ```
  scalaOrganization := "org.typelevel"
  ```

If this does resolve the problem, please lend your support to the [pull request][si-7046-pr] being merged in Lightbend
Scala.

[tls]: https://github.com/typelevel/scala
[si-7046-pr]: https://github.com/scala/scala/pull/5284

### shapeless-2.3.2 with Maven

shapeless is also available for projects using the Maven build tool via the following dependency,

```xml
<dependency>
  <groupId>com.chuusai</groupId>
  <artifactId>shapeless_2.11</artifactId>
  <version>2.3.2</version>
</dependency>
```

If you are using Scala 2.10.x, you should also add the macro paradise plugin to your build,

```xml
<dependency>
  <groupId>com.chuusai</groupId>
  <artifactId>shapeless_2.10</artifactId>
  <version>2.2.5</version>
</dependency>

<plugins>
  ...
  <plugin>
    ...
    <configuration>
      ...
      <compilerPlugins>
        <compilerPlugin>
          <groupId>org.scala-lang.plugins</groupId>
          <artifactId>macro-paradise_2.10</artifactId>
          <version>2.1.0</version>
        </compilerPlugin>
      </compilerPlugins>
      ...
    </configuration>
    ...
  </plugin>
  ...
</plugins>
```

### Older releases

Please use a current release if possible. If unavoidable, you can find [usage information for older
releases][olderusage] on the shapeless wiki.

[olderusage]: https://github.com/milessabin/shapeless/wiki/Using-shapeless:-older-releases

## Building shapeless

shapeless is built with SBT 0.13.13 or later, and its master branch is built with Scala 2.12.1 by default but also
cross-builds for 2.10.6 and 2.11.8.

[namehashing]: https://github.com/sbt/sbt/issues/1640

## Contributors

+ Alessandro Lacava <alessandrolacava@gmail.com> [@lambdista](https://twitter.com/lambdista)
+ Alexander Konovalov <alex.knvl@gmail.com> [@alexknvl](https://twitter.com/alexknvl)
+ Alexandre Archambault <alexandre.archambault@gmail.com> [@alxarchambault](https://twitter.com/alxarchambault)
+ Alistair Johnson <alistair.johnson@johnsonusm.com> [@AlistairUSM](https://twitter.com/AlistairUSM)
+ Alois Cochard <alois.cochard@gmail.com> [@aloiscochard](https://twitter.com/aloiscochard)
+ Andreas Koestler <andreas.koestler@gmail.com> [@AndreasKostler](https://twitter.com/AndreasKostler)
+ Andrew Brett <github@bretts.org> [@Ephemerix](https://twitter.com/Ephemerix)
+ Arya Irani <arya.irani@gmail.com> [@aryairani](https://twitter.com/aryairani)
+ Ben Hutchison <brhutchison@gmail.com> [@ben_hutchison](https://twitter.com/ben_hutchison)
+ Ben James <ben.james@guardian.co.uk> [@bmjames](https://twitter.com/bmjames)
+ Brian McKenna <brian@brianmckenna.org> [@puffnfresh](https://twitter.com/puffnfresh)
+ Brian Zeligson <brian.zeligson@gmail.com> [@beezee](https://twitter.com/bzeg)
+ Bryn Keller <xoltar@xoltar.org> [@brynkeller](https://twitter.com/brynkeller)
+ Chris Hodapp <clhodapp1@gmail.com> [@clhodapp](https://twitter.com/clhodapp)
+ Cody Allen <ceedubs@gmail.com> [@fourierstrick](https://twitter.com/fourierstrick)
+ Dale Wijnand <dale.wijnand@gmail.com> [@dwijnand](https://twitter.com/dwijnand)
+ Daniel Urban <urban.dani@gmail.com>
+ Dario Rexin <dario.rexin@r3-tech.de> [@evonox](https://twitter.com/evonox)
+ Dave Gurnell <d.j.gurnell@gmail.com> [@davegurnell](https://twitter.com/davegurnell)
+ David Barri <japgolly@gmail.com> [@japgolly](https://twitter.com/japgolly)
+ Denis Mikhaylov <notxcain@gmail.com> [@notxcain](https://twitter.com/@notxcain)
+ Eugene Burmako <xeno.by@gmail.com> [@xeno_by](https://twitter.com/xeno_by)
+ Filipe Nepomuceno <filinep@gmail.com>
+ Frank S. Thomas <frank@timepit.eu> [@fst9000](https://twitter.com/fst9000)
+ George Leontiev <folone@gmail.com> [@folone](https://twitter.com/folone)
+ Hamish Dickenson <hamish.dickson@gmail.com> [@hamishdickson](https://twitter.com/hamishdickson)
+ Howard Branch <purestgreen@gmail.com> [@purestgreen](https://twitter.com/purestgreen)
+ Huw Giddens <hgiddens@gmail.com>
+ Ievgen Garkusha <ievgen@riskident.com>
+ Jason Zaugg <jzaugg@gmail.com> [@retronym](https://twitter.com/retronym)
+ Jean-Remi Desjardins <jeanremi.desjardins@gmail.com> [@jrdesjardins](https://twitter.com/jrdesjardins)
+ Jeff Wilde <jeff@robo.ai>
+ Jeremy R. Smith <jeremyrsmith@gmail.com> [@jeremyrsmith](https://twitter.com/jeremyrsmith)
+ Jisoo Park <xxxyel@gmail.com> [@guersam](https://twitter.com/guersam)
+ Johannes Rudolph <johannes.rudolph@gmail.com> [@virtualvoid](https://twitter.com/virtualvoid)
+ Johnny Everson <khronnuz@gmail.com> [@johnny_everson](https://twitter.com/johnny_everson)
+ Jolse Maginnis jolse.maginnis@pearson.com [@doolse2](https://twitter.com/doolse2)
+ Joni Freeman <joni.freeman@ri.fi> [@jonifreeman](https://twitter.com/jonifreeman)
+ Joseph Price <josephprice@iheartmedia.com>
+ Julien Tournay <boudhevil@gmail.com> [@skaalf](https://twitter.com/skaalf)
+ Jules Gosnell <jules_gosnell@yahoo.com>
+ Kailuo Wang <kailuo.wang@gmail.com> [@kailuowang](https://twitter.com/kailuowang)
+ Kenji Yoshida <6b656e6a69@gmail.com> [@xuwei_k](https://twitter.com/xuwei_k)
+ Kevin Wright <kev.lee.wright@gmail.com> [@thecoda](https://twitter.com/thecoda)
+ Lars Hupel <lars.hupel@mytum.de> [@larsr_h](https://twitter.com/larsr_h)
+ Mario Pastorelli <mario.pastorelli@teralytics.ch> [@mapastr](https://twitter.com/mapastr)
+ Matthew Taylor <matthew.t@tbfe.net>
+ Mathias Doenitz <mathias@spray.io> [@sirthias](https://twitter.com/sirthias)
+ Michael Donaghy <md401@srcf.ucam.org>
+ Michael Pilquist <mpilquist@gmail.com> [@mpilquist](https://twitter.com/mpilquist)
+ Miles Sabin <miles@milessabin.com> [@milessabin](https://twitter.com/milessabin)
+ Neville Li <neville@spotify.com> [@sinisa_lyh](https://twitter.com/sinisa_lyh)
+ Nikolas Evangelopoulos <nikolas@jkl.gr>
+ Oleg Aleshko <olegych@tut.by> [@OlegYch](https://twitter.com/OlegYch)
+ Olivier Blanvillain <olivier.blanvillain@gmail.com>
+ Olli Helenius <liff@iki.fi> [@ollijh](https://twitter.com/ollijh)
+ Owein Reese <owreese@gmail.com> [@OweinReese](https://twitter.com/OweinReese)
+ Paolo G. Giarrusso <p.giarrusso@gmail.com> [@blaisorblade](https://twitter.com/blaisorblade)
+ Pascal Voitot <pascal.voitot.dev@gmail.com> [@mandubian](https://twitter.com/mandubian)
+ Pavel Chlupacek <pavel.chlupacek@spinoco.com> [@pacmanius](https://twitter.com/pacmanius)
+ Peter Neyens <peter.neyens@gmail.com> [@pneyens](https://twitter.com/pneyens)
+ Peter Schmitz <petrischmitz@gmail.com> [@peterschmitz\_](https://twitter.com/peterschmitz_)
+ Renato Cavalcanti <renato@strongtyped.io> [@renatocaval](https://twitter.com/renatocaval)
+ Rob Norris <rob_norris@mac.com> [@tpolecat](https://twitter.com/tpolecat)
+ Robert Hensing <spam@roberthensing.nl>
+ Ryo Hongo <ryoppy0516@gmail.com> [@ryoppy516](https://twitter.com/ryoppy516)
+ Sam Halliday <sam.halliday@gmail.com> [@fommil](https://twitter.com/fommil)
+ Sarah Gerweck <sarah.a180@gmail.com> [@SGerweck](https://twitter.com/SGerweck)
+ Sébastien Doeraene <sjrdoeraene@gmail.com> [@sjrdoeraene](https://twitter.com/sjrdoeraene)
+ Simon Hafner <hafnersimon@gmail.com> [@reactormonk](https://twitter.com/reactormonk)
+ Stacy Curl <stacy.curl@gmail.com> [@stacycurl](https://twitter.com/stacycurl)
+ Stephen Compall <scompall@nocandysw.com> [@S11001001](https://twitter.com/S11001001)
+ Tin Pavlinic <tin.pavlinic@gmail.com> [@triggerNZ](https://twitter.com/triggerNZ)
+ Tom Switzer <thomas.switzer@gmail.com> [@tixxit](https://twitter.com/tixxit)
+ Tomas Mikula <tomas.mikula@gmail.com> [@tomas_mikula](https://twitter.com/tomas_mikula)
+ Travis Brown <travisrobertbrown@gmail.com> [@travisbrown](https://twitter.com/travisbrown)
+ Valentin Kasas <valentin.kasas@gmail.com> [@ValentinKasas](https://twitter.com/ValentinKasas)
+ Valerian Barbot <valerian.barbot@onzo.com> [@etaty](https://twitter.com/etaty)
+ Vladimir Matveev <vladimir.matweev@gmail.com> [@netvlm](https://twitter.com/netvlm)
+ Vladimir Pavkin <vpavkin@gmail.com> [@vlpavkin](https://twitter.com/vlpavkin)
+ Yang Bo (杨博) <pop.atry@gmail.com> [@Atry](https://twitter.com/Atry)
