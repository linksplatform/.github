# LinksPlatform ([русская версия](https://github.com/Konard/LinksPlatform/blob/master/README.ru.md))

The Links Platform is a [modular](https://en.wikipedia.org/wiki/Modular_programming) [framework](https://en.wikipedia.org/wiki/Software_framework) (each [library](https://en.wikipedia.org/wiki/Library_(computing)) of this [framework](https://en.wikipedia.org/wiki/Software_framework) can be used separately), that includes two [DBMS](https://en.wikipedia.org/wiki/Database#Database_management_system) [implementations](https://en.wikipedia.org/wiki/Software_implementation) based on [the associative data model](https://en.wikipedia.org/wiki/Associative_model_of_data): [Doublets](https://github.com/linksplatform/Data.Doublets) and [Triplets](https://github.com/linksplatform/Data.Triplets); as well as [translators](https://en.wikipedia.org/wiki/Translator_(computing)) (for example [from C# to C++](https://github.com/linksplatform/RegularExpressions.Transformer.CSharpToCpp)) and [bot](https://github.com/linksplatform/Bot).

At the moment we use [C#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language)), [C++](https://en.wikipedia.org/wiki/C%2B%2B), [C](https://en.wikipedia.org/wiki/C_(programming_language)), [JavaScript](https://en.wikipedia.org/wiki/JavaScript), [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) [programming languages](https://en.wikipedia.org/wiki/Programming_language), and [Rust](https://en.wikipedia.org/wiki/Rust_(programming_language)).

[Documentation](http://linksplatform.github.io/Documentation)

[![introduction](https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/Intro/intro-animation-500.gif "introduction")](https://github.com/Konard/LinksPlatform/wiki/How-it-all-began)

[Graphical introduction](https://github.com/Konard/LinksPlatform/wiki/How-it-all-began)

## [Quick start example](https://github.com/linksplatform/Examples.Doublets.CRUD.DotNet) | [Run .NET fiddle](https://dotnetfiddle.net/Y7Zvt0)

```C#
using System;
using Platform.Data;
using Platform.Data.Doublets;
using Platform.Data.Doublets.Memory.United.Generic;

// A doublet links store is mapped to "db.links" file:
using var links = new UnitedMemoryLinks<uint>("db.links");

// A creation of the doublet link: 
var link = links.Create();

// The link is updated to reference itself twice (as a source and a target):
link = links.Update(link, newSource: link, newTarget: link);

// Read operations:
Console.WriteLine($"The number of links in the data store is {links.Count()}.");
Console.WriteLine("Data store contents:");
var any = links.Constants.Any; // Means any link address or no restriction on link address
// Arguments of the query are interpreted as restrictions
var query = new Link<uint>(index: any, source: any, target: any);
links.Each((link) => {
    Console.WriteLine(links.Format(link));
    return links.Constants.Continue;
}, query);

// The link's content reset:
link = links.Update(link, newSource: default, newTarget: default);

// The link deletion:
links.Delete(link);
```

## [SQLite vs Doublets](https://github.com/linksplatform/Comparisons.SQLiteVSDoublets)

[![Image with result of performance comparison between SQLite and Doublets.](https://raw.githubusercontent.com/linksplatform/Documentation/master/doc/Examples/sqlite_vs_doublets_performance.png "Result of performance comparison between SQLite and Doublets")](https://github.com/linksplatform/Comparisons.SQLiteVSDoublets)

## Description

Inspired by the work of [Simon Williams](https://uk.linkedin.com/in/s1m0n) ([The Associative Model of Data](https://web.archive.org/web/20210814063207/https://en.wikipedia.org/wiki/Associative_model_of_data)), [book](https://web.archive.org/web/20181219134621/http://sentences.com/docs/amd.pdf), [whitepaper](http://iacis.org/iis/2009/P2009_1301.pdf).

[Comparison](https://en.wikipedia.org/wiki/Comparison) of [models](https://en.wikipedia.org/wiki/Data_model):

![Comparison of models](https://github.com/LinksPlatform/Documentation/raw/master/doc/ModelsComparison/relational_model_vs_associative_model_vs_links.png)

[Comparison](https://en.wikipedia.org/wiki/Comparison) of [theories](https://en.wikipedia.org/wiki/Theory):

![Comparison of theories](https://github.com/LinksPlatform/Documentation/raw/master/doc/TheoriesComparison/theories_comparison_en.png)

This platform uses a unified [data type](https://en.wikipedia.org/wiki/Data_type) — link, which is a combination of `Item` and `Link` from a work by [Simon Williams](https://uk.linkedin.com/in/s1m0n). So the `Item` or [Point](https://en.wikipedia.org/wiki/Point) is a specific case of the [link, which references itself](http://linksplatform.github.io/itself.html).

There are two variants of Link [structure](https://en.wikipedia.org/wiki/Data_structure):

> <img src="https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/ST-dots.png" width="400" title="Source-Target link, untyped" alt="Source-Target link, untyped" />
> <img src="https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/doublet-colored.png" width="400" title="Source-Target link, untyped" alt="Source-Target link, untyped" />

- [Untyped](https://en.wikipedia.org/wiki/Type_theory), each link contains [Source](https://en.wikipedia.org/wiki/Source) ([beginning](https://en.wikipedia.org/wiki/Begin), [start](https://en.wikipedia.org/wiki/Start), [first](https://en.wikipedia.org/wiki/First), [left](https://en.wikipedia.org/wiki/Left), [subject](https://en.wikipedia.org/wiki/Subject)) and [Target](https://en.wikipedia.org/wiki/Target) ([ending](https://en.wikipedia.org/wiki/End), [stop](https://en.wikipedia.org/wiki/Stop), [last](https://en.wikipedia.org/wiki/Last_(disambiguation)), [right](https://en.wikipedia.org/wiki/Right_(disambiguation)), [predicate](https://en.wikipedia.org/wiki/Predicate), [object](https://en.wikipedia.org/wiki/Object)).

> <img src="https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/SLT-dots.png" width="400" title="Source-Linker-Target link, typed" alt="Source-Linker-Target link, typed" />
> <img src="https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/triplet-colored.png" width="400" title="Source-Linker-Target link, typed" alt="Source-Linker-Target link, typed" />

- [Typed](https://en.wikipedia.org/wiki/Type_theory) ([semantic](https://en.wikipedia.org/wiki/Semantics)), with added [Linker](https://en.wikipedia.org/wiki/Linker) ([verb](https://en.wikipedia.org/wiki/Verb), [action](https://en.wikipedia.org/wiki/Action_(philosophy)), [type](https://en.wikipedia.org/wiki/Type_system), [category](https://en.wikipedia.org/wiki/Category_theory), [predicate](https://en.wikipedia.org/wiki/Predicate), [transition](https://en.wikipedia.org/wiki/Transition_system), [algorithm](https://en.wikipedia.org/wiki/Algorithm)), so any additional [information](https://en.wikipedia.org/wiki/Information) about a [type](https://en.wikipedia.org/wiki/Type_theory) of [connection](https://en.wikipedia.org/wiki/Association_(psychology)) between two links can be [stored](https://en.wikipedia.org/wiki/Data_storage) here.

Links Platform [planned](https://en.wikipedia.org/wiki/Plan) as a [system](https://en.wikipedia.org/wiki/System_(disambiguation)), that [combines](https://en.wikipedia.org/wiki/Combine) simple [associative memory](https://en.wikipedia.org/wiki/Associative_memory) [storage](https://en.wikipedia.org/wiki/Computer_data_storage) (Links) and [transformation](https://en.wikipedia.org/wiki/Transformation) [execution](https://en.wikipedia.org/wiki/Execution_(computing)) [engine](https://en.wikipedia.org/wiki/Database_engine) (Triggers). There will be an ability to [program](https://en.wikipedia.org/wiki/Program_(machine)) that [system](https://en.wikipedia.org/wiki/System_(disambiguation)) dynamically, due to the [fact](https://en.wikipedia.org/wiki/Fact) that all [algorithms](https://en.wikipedia.org/wiki/Algorithm) will be treated as [data](https://en.wikipedia.org/wiki/Data_(disambiguation)) inside the [storage](https://en.wikipedia.org/wiki/Computer_data_storage). Such [algorithms](https://en.wikipedia.org/wiki/Algorithm) can also change themselves in [real-time](https://en.wikipedia.org/wiki/Real-time) based on [input](https://en.wikipedia.org/wiki/Input) from the [environment](https://en.wikipedia.org/wiki/Environment). The Links Platform is a [method](https://en.wikipedia.org/wiki/Method) of [modeling](https://en.wikipedia.org/wiki/Data_modeling) the high-level [associative memory](https://en.wikipedia.org/wiki/Associative_memory) [effects](https://en.wikipedia.org/wiki/Effect) of [human](https://en.wikipedia.org/wiki/Human) [mind](https://en.wikipedia.org/wiki/Mind).

We strive to make our [implementation](https://en.wikipedia.org/wiki/Implementation) of [associative](https://en.wikipedia.org/wiki/Associative_memory) [storage](https://en.wikipedia.org/wiki/Data_storage) the most accurate, simple, universal, flexible, reliable and fast [memory](https://en.wikipedia.org/wiki/Memory) [implementation](https://en.wikipedia.org/wiki/Implementation) for any [data](https://en.wikipedia.org/wiki/Data) and [knowledge](https://en.wikipedia.org/wiki/Knowledge).

One of the most important [goals](https://en.wikipedia.org/wiki/Goal) of the [project](https://en.wikipedia.org/wiki/Project) is to accelerate the [development](https://en.wikipedia.org/wiki/Software_development) of [automation](https://en.wikipedia.org/wiki/Automation) to the level when [automation](https://en.wikipedia.org/wiki/Automation) can be itself [automated](https://en.wikipedia.org/wiki/Automation). In other words, this [project](https://en.wikipedia.org/wiki/Project) should help to [implement](https://en.wikipedia.org/wiki/Software_implementation)) a [bot-programmer](https://en.wikipedia.org/wiki/Internet_bot) which will be able to create [programs](https://en.wikipedia.org/wiki/Computer_program) based on descriptions in [human](https://en.wikipedia.org/wiki/Human) [language](https://en.wikipedia.org/wiki/Language).

## [Road map](https://en.wikipedia.org/wiki/Technology_roadmap)
[![Road Map, Status](https://raw.githubusercontent.com/LinksPlatform/Documentation/master/doc/RoadMap-status.png "Road Map, Status")](https://github.com/orgs/linksplatform/projects)

[Project status](https://github.com/orgs/linksplatform/projects)

## [Frequently asked questions](https://github.com/Konard/LinksPlatform/wiki/FAQ)

## [Support](https://en.wikipedia.org/wiki/Technical_support)

Ask questions at [stackoverflow.com/tags/links-platform](https://stackoverflow.com/tags/links-platform) (or with tag `links-platform`) to get our free [support](https://en.wikipedia.org/wiki/Technical_support).

You can also get [real-time](https://en.wikipedia.org/wiki/Real-time) [support](https://en.wikipedia.org/wiki/Technical_support) on [our official Discord server](https://discord.gg/eEXJyjWv5e).

## Contacts

[vk.com/linksplatform](https://vk.com/linksplatform)

[vk.com/konard](https://vk.com/konard)
