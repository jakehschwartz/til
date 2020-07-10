# Adding Scapegoat To IntelliJ's Build Process

At [work](zignallabs.com/), we have been using [Scapegoat](https://github.com/sksamuel/scapegoat)
with [sbt](https://www.scala-sbt.org/) to check for code smells. Scapegoat is a static code analyzer 
that has an [sbt plugin](https://github.com/sksamuel/sbt-scapegoat) and we are using that to do our
analysis on our build server. While it is possible to run locally as well, it is not built into
[IntelliJ](https://www.jetbrains.com/idea/), which is what our team uses to develop all of our Scala
codebases. Because it does not run whenever we compile, it is sometimes neglected to be run before 
checking in a change and developers, myself included, have to go back and make the appropriate changes.

To include this in the compile stage, we will take advantage of the sbt plugin:

```
// plugins.sbt
addSbtPlugin("com.sksamuel.scapegoat" %% "sbt-scapegoat" % "1.0.9")
```

Then, we will create a separate sbt file for scapegoat, enable the compiler plugin and then
configure the scapegoat settings:

```
// scapegoat.sbt
addCompilerPlugin("com.sksamuel.scapegoat" % "scalac-scapegoat-plugin_2.12.10" % "1.4.0")

scapegoatVersion in ThisBuild := "1.3.11"

scapegoatDisabledInspections := Seq(
  "AsInstanceOf",
)

scalacOptions ++= Seq(
  "-P:scapegoat:dataDir:./target/scapegoat"
) ++ scapegoatDisabledInspections.value.map(x => s"-P:scapegoat:disabledInspections:$x" )
```

The examples above may not be the most up-to-date versions, but you get the point. The second part
about the disable inspections is also not required, but it a nice way to define the list in a
'nice' way using the sbt plugin and easily converting it to being using by the compiler plugin. The
only required part is the `-P:scapegoat:dataDir` scalac option. Once you add this, you should see
Scapegoat errors show up during both IntelliJ builds and when compiling through sbt.
