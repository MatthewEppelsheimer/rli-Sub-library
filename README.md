# Subspace: an easy way to namespace shell commands

Subspace is based on Sub (add link), a model for creating shell programs that use subcommands. Subspace improves Sub by allowing you to create as many shell commands as you would like within a given subspace. You can use your commands by adding your subspace to your path or by activating your subspace with `source`.

## Entering Subspace

Subspace comes with these commands:

* `sub commands [-l]`: Lists documented subcommands
* `sub help [<subcommand>]`: Documents how to use a subcommand
* `sub launch <command>`: Creates a new executable ready for subcommands
* `sub list`: Lists commands in your subspace

## Mapping Subspace

Your subspace looks like this:

    .
    ├── bin               # Links to your commands
    ├── libexec           # Your commands and subcommands
    └── share             # Anything else you might need to store

`libexec` contains your subspace library, or the executables for your commands and subcommands. 

`bin` contains symbolic links to the commands in your subspace library. Launching a new command into your subspace will automatically create a file in `bin` that links to an executable in `libexec` (you can also do this manually if you prefer). You can run the commands in `bin` from your terminal by adding your subspace's `bin` directory to your shell PATH variable (more info below). 

`share` is a space for you to store anything else your commands might need (for example, config files).

## Launching Commands into Subspace

All commands in your subspace use the format:
    
    $ <command> <subcommand> [<args>]

Running `sub launch <command>` will add a new command to your subspace, along with the default `commands` and `help` subcommands. You can add more subcommands by placing executables in your subspace's `libexec` directory. Subcommand file names must take the format of `<command>-<subcommand>`. You can write subcommands in any language you want as long as they exist as executables in `libexec`.

## Developing Subcommands

Subspace provides a few variables to use in your subcommands:

* `SUB_ROOT`: Path to the root of your subspace
* `SUB_COMMAND`: Stores the command that was executed

## Documenting Subcommands

Subspace allows for self-documenting subcommands. All you need to do is comment your subcommands in the format below.

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

Subcommands documented this way will print summary, usage, and help info wheny you run `$ <command> help <subcommand>`.

## Running Your Commands

There are three ways to run the commands in your subspace:

1. Add your subspace `bin` directory to your shell PATH variable
2. Use the command's full or relative path
3. Activate your subspace within a given terminal

### Adding Subspace to Shell Path

1. Open the file `.bashrc` in your home directory. If it doesn't exist, create it.
2. Find the line that says:

    `export PATH=/a/bunch/of/paths/to/export:$PATH`

3. Add your subspace `bin` path to the beginning of the PATH variable, for example:

    `export PATH=/path/to/subspace/bin:/a/bunch/of/paths/to/export:$PATH`

    If your file does not export the PATH variable, create and export it, for example:

    `export PATH=/path/to/subspace/bin:$PATH`

4. Restart your terminal by closing and reopening it, or by running `source ~/.bash_rc`

You should now be able to run commands in your subspace from your restarted terminal and from any new terminal you open.

### Run Command Using Its Path

You can run your command using it's full or relative path. For example:

`$ /home/path/to/subspace/bin/command` or `$ ./relative/path/to/subspace/bin/command`

### Activating Your Subspace

You can activate your subspace within a given terminal by running `source` on the path to your subspace `activate` command. For example,

`$ source /home/path/to/subspace/activate` or `$ source ./relative/path/to/subspace/active`

This can be useful if you would like to test commands for a subspace that you are developing but do not want those commands to permanently exist on your shell path, or do not want those commands to permanently override shell commands with the same name. 

## Naming Your Subspace

Details to come...

## License

MIT. See `LICENSE`.
