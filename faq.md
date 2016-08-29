---
title: "ScalaPB: Frequently Asked Questions"
layout: page
---

# Frequently Asked Questions

## IntelliJ complains on duplicate files ("class is already defined")

SBT-protobuf which ScalaPB relies on defaults to generating the case
classes in `target/src_managed/compiled_protobuf/`.  This leads to a situation
where both `target/src_managed/compiled_protobuf/` and its parent, `target/src_managed/`, 
are considered source directories and the source files are seen twice. To
eliminate this problem, let's tell sbt-protobuf to generate the sources into
the parent directory. Add this to your `build.sbt`:

{%highlight scala%}
scalaSource in PB.protobufConfig := sourceManaged.value
{%endhighlight%}

If you generate Java sources, add,

{%highlight scala%}
javaSource in PB.protobufConfig := sourceManaged.value
{%endhighlight%}