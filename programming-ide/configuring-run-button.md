# Configuring the "Run" button

A file named `.replit` can be added to any repl in order to customize the behavior of the "Run" button. Written in [toml](https://github.com/toml-lang/toml), a `.replit` file looks something like:

```toml
run = "<run command here>"
language = "<repl language>" # optional
```

In the snippet above, `run` is a string which will be executed in the shell whenever you hit the "Run" button. The `language` helps the IDE understand how to provide features like [packaging](https://blog.replit.com/upm) and [code intelligence](https://blog.replit.com/intel). This is normally configured for you when you clone from a Git repository.

Here is an example of a repl using `.replit` to print "hello world" instead of running the code:

<iframe width="100%" src="https://replit.com/@turbio/dotreplit-example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

## Configuring a Cloned Repl

When you clone a repository without a `.replit` file, we automatically show the visual `.replit` editor:

![visual config editor](https://docs.replit.com/images/config_plugin.png)

This will automatically create the `.replit` file and make it possible to customize how the repl will run. You can use the shell to run any command and then set the "Run" button once you've decided what it should do. Clicking "done" will finalize the repl's configuration and close the visual editor. It's always possible to make changes later by visiting the `.replit` file from the filetree. Adding `.replit` to a repository makes cloning fast with no configuration necessary. 

# Other Configuration
The `.replit` file can also provide other configuration hints. The full specification is provided below:
- `run`: Command that is executed when the run button is clicked
- `language`: Reserved
- `onBoot`: Command that is executed once when the repl first starts up
- `audio`: Whether [system-wide audio](https://docs.replit.com/misc/playing-audio-replit) is enabled for this repl.
- `packager.afterInstall`: Command that is executed after a new package is installed
- `packager.ignoredPaths`: List of paths to ignore while attempting to guess packages ([More about installing packages](https://docs.replit.com/repls/packages/#DirectImports))
- `packager.ignoredPackages`: List of modules to never attempt to guess a package for, when installing packages ([More about installing packages](https://docs.replit.com/repls/packages/#DirectImports))

## Example .replit File

```toml
run="python main.py"
language="python3"
onBoot="echo Booting up!"

[packager]
afterInstall="date >> package_install_log"
ignoredPaths=[".git"]
ignoredPackages=["twitter", "discord"]
```

## HTML

For HTML projects, you can keep the run command empty and we will serve the project for you automatically. As per web standards, the entrypoint file is `index.html`. If you want to serve a different file, you can roll your own webserver in one of the languages that we support. 

We created an [example](https://replit.com/@amasad/run-html-non-index-file) for you in NodeJS that serves `foo.html` instead of `index.html`. Otherwise it works like any other HTML project.
