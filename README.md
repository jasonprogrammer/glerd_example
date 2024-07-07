# Glerd Tutorial

This is an example [Gleam](https://gleam.run/) project to help demonstrate how
to use [Glerd](https://github.com/darky/glerd), a library that can generate
metadata for [Records](https://tour.gleam.run/data-types/records/) in Gleam.

## Instructions

1. Clone this repository:

```
git clone https://github.com/jasonprogrammer/glerd_example.git
```

2. Change into the `glerd_example` directory:

```
cd glerd_example
```

3. Install glerd as a development dependency:

```
gleam run -m glerd
```

4. After running this, you'll notice that Glerd has created a
`src/glerd_gen.gleam` file locally. The file looks like this:

```
// this file was generated via "gleam run -m glerd"

import glerd/types

pub const record_info = [
  #(
    "User",
    "user",
    [
      #("id", types.IsInt), #("name", types.IsString),
      #("email", types.IsString),
    ],
    "",
  ),
]
```

This file was created as a result of Glerd scanning the `src` directory,
finding the `user.gleam` file:

```
pub type User {
  User(id: Int, name: String, email: String)
}
```

and generating the `glerd_gen.gleam` metadata file.

## How can we use this perpetually in a project?

There are multiple ways of doing this. Here's one possibiity. We could:

1. Add the `glerd_gen.gleam` as code to a project (e.g. add to Git source
control with the other source files).

2. Clone the [Glerd](https://github.com/darky/glerd) repository and build a
single binary of Glerd using [Gleescript](https://hexdocs.pm/gleescript/).
Add this binary to the project repo so that we can run the Gleescript binary
each time we build the Gleam project (e.g. before running `gleam run`).

Creating a single binary helps us avoid adding all of Glerd's dependencies to
our project, and helps us avoid rebuilding Glerd code each time we want to
invoke it.

