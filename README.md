# Subspace: an easy way to namespace shell commands

Subspace is based on Sub (add link), a model for creating shell programs that use subcommands. Subspace improves upon Sub by allowing you to create as many shell commands as you would like within a given subspace. You can use your commands by adding your subspace to your path or by activating your subspace with `source`.

## Entering Subspace

Subspace comes with these commands:

* `sub commands [-l]`: List documented subcommands
* `sub help [<subcommand>]`: Document how to use a subcommand
* `sub launch <command>`: Create a new executable ready for subcommands
* `sub lib`: List commands in your subspace

## Launch Commands

Running `sub launch <command>` will add a new command to your subspace, along with `commands` and `help` subcommands. You can add more subcommands by placing executables in the `subspace/libexec` directory in the format of `<command>-<subcommand>`. Your subcommands can be in any language you want as long as they run.

All commands in your subspace will use the format of:
    
    $ <command> <subcommand> [<args>]

## Mapping Subspace

Each subcommand maps to a separate, standalone executable program. Sub programs are laid out like so:

    .
    ├── bin               # Your commands
    ├── libexec           # Your subcommands
    └── share             # Anything else you might need to store

## Developing Subcommands

Subspace provides a few variables to use in your subcommands:

* `_SUB_ROOT`: Path to the root of your subspace
* `SUB_COMMAND`: Stores the command that was executed

## Documenting Subcommands

Subspace allows for self-documenting subcommands when. All you need to do is comment your subcommands in the format below.

```
#!/usr/bin/env bash
# Usage: <command> <subcommand> [options]
# Summary: Put a short summary here.
# Help: Help info can be longer.
# You can even have multiple lines!
#
#    Show off an example indented
#
# And maybe start off another one?
```

Now, running `$ <command> help <subcommand>` will print summary, usage, and help info.

## Running Your Command

(Adding to PATH, activation, or just running)

## License

MIT. See `LICENSE`.
