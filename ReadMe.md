# MUSTACHE-ZIG
[![made with Zig](https://img.shields.io/badge/made%20with%20%E2%9D%A4%20-Zig-orange)]()
[![license mit](https://img.shields.io/github/license/batiati/mustache-zig)]()

Mustache-Zig is an implementation of the [{{mustache}} template system](https://mustache.github.io/) for [Zig](https://ziglang.org/).

![logo](mustache.png)

# ! Under development !

## Samples

Render from strings, files and cached templates.
See the [source code](https://github.com/batiati/mustache-zig/tree/master/samples) for more details.

## Full spec compliant

- Supports most of elements from [mustache spec](https://github.com/mustache/spec) with all tests passing ✔️.

delimiters: `{{=[]=}}`

interpolation: `{{name}}`

unescaped interpolation: `{{&name}}` and `{{{name}}}`

sections: `{{#items}}` and `{{/items}}`

inverted sections: `{{^finished}}` and `{{/finished}}`

comments: `{{! blah blah }}`


- Partials and inheritance comming soon ...

partials: `{{>partial}}`

parent: `{{<parent}}`

blocks: `{{$block}}`


## Designed for low memory consumption.

Mustache templates are well known for HTML templating, but it's useful to render any kind of dynamic document, and potentially load templates from untrusted or user-defined sources.

So, it's important to be able to deal with multi-megabyte inputs without eating all your RAM.

```Zig

    // 16KB should be enough memory for this job
    var plenty_of_memory = std.heap.GeneralPurposeAllocator(.{ .enable_memory_limit = true }){
        .requested_memory_limit = 16 * 1024,
    };
    defer _ = plenty_of_memory.deinit();

    try mustache.renderFromFile(plenty_of_memory.allocator(), "10MB_file.mustache", ctx, out_writer);

```

## Licensing

- MIT

- Mustache is Copyright (C) 2009 Chris Wanstrath
Original CTemplate by Google