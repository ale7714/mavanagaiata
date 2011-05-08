Mavanagaiata
============

Mavanagaiata – \[maˈvanaˈɡaːjaˈta\] – is a Maven plugin providing information
about the Git repository of your project.

## Requirements

 * Maven 2.0+

## Dependencies

 * JGit 0.12.1

## Installation

Mavanagaiata is available from the Central Reposioty and will be automatically
installed by Maven once you add it as a plugin to your project. If you want to
have the newest features available in the development code or you want to hack
on the code you are free to clone the Git repository and install it manually.
You can do so using the following commands:

```bash
$ git clone git://github.com/koraktor/mavanagaiata.git
$ cd mavanagaiata
$ mvn install
```

## Usage

To use the Mavanagaiata plugin in your Maven project you will have to include
the plugin in your POM and add the configuration suitable for your needs:

```xml
<project ...>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>com.github.koraktor</groupId>
                <artifactId>mavanagaiata</artifactId>
                <executions>
                    <execution>
                        <id>load-git-branch</id>
                        <goals>
                            <goal>branch</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            ...
        </plugins>
        ...
    </build>
</project>
```

### Goals

Mavanagaiata provides the following goals each reading specific information from
the Git repository.

 * `branch`:       Information about the currently checked out branch
 * `changelog`:    Generates a changelog from Git commits and tags
 * `commit`:       Information about the current commit
 * `contributors`: Generates a list of contributors from Git commits
 * `tag`:          Information about the most recent tag

Each goal stores its information into the project's properties. The following
property keys will be prefixed with `mavanagaiata.` and `mvngit.` respectively.
You may override this with the configuration property `propertyPrefixes`.

 * `branch`
   * `branch`: The name of the currently checked out branch
 * `commit`
   * `abbrev`:          The abbreviated SHA ID of the current commit
   * `author.date`:     The date the commit has been authored
   * `author.name`:     The name of the author of the current commit
   * `author.email`:    The email address of the author of the current commit
   * `committer.date`:  The date the commit has been committed
   * `committer.name`:  The name of the committer of the current commit
   * `committer.email`: The email address of the committer of the current
                        commit
   * `id` / `sha`:      The full SHA ID of the current commit
 * `tag`
   * `name`:     The name of the most recent tag (if any)
   * `describe`: A combination of the tag name and the current commit ID
     (same as `git describe`)

### Configuration

Mavanagaiata provides several configuration properties for its goals. The
following ones are global and can be used for any goal. They must be prefixed
with `mavanagaiata.`:

 * `gitDir`: Specify the GIT_DIR to use (default: `${basedir}/.git`)
 * `head`:   Specify the commit or ref used as a starting point (default:
             `HEAD`)

Additionally, there are some properties specific to a goal:

 * `changelog` (prefix: `mavanagaiata.changelog.`):
   * `dateFormat`:   The date format to use for tag output (default
                    `"MM/dd/yyyy hh:mm a Z"`)
   * `header`:       The header to print above the changelog (default:
                     `"Changelog\n=========\n"`)
   * `commitPrefix`: The string to prepend to every commit message (default:
                     `" * "`)
   * `outputFile`:   If set, the changelog will not be printed to `System.out`,
                     but into the given file. (default: not set)
   * `skipTagged`:   Whether to skip tagged commits' messages. This is useful
                     when usually tagging commits like "Version bump to X.Y.Z"
                     (default: `false`)
   * `tagPrefix`:    The string to prepend to the tag name (default:
                     `"\nVersion "`)
 * `commit` (prefix: `mavanagaiata.commit.`):
   * `dateFormat`: The date format to use for commit dates (default
                    `"MM/dd/yyyy hh:mm a Z"`)
 * `contributors` (prefix: `mavanagaiata.contributors.`):
   * `header`:     The header to print above the contributor list (default:
                   `"Contributors\n============\n"`)
   * `outputFile`: If set, the list will not be printed to `System.out`, but
                   into the given file. (default: not set)
   * `showCounts`: Whether to show the number of contributions for each author
                   (default: `true`)
   * `showEmail`:  Whether to show the email addresses of contributors
                   (default: `false`)

## About the name

The name is a completely invented word hopefully sounding like a mighty god of
an ancient, Southeast Asian primitive people or a similar mighty monster that
same primitive people is afraid of.

Instead, it's just a combination of the command-line tools of Maven and Git:
`mvn` and `git`. Each character is suffixed with the character `a`.

In Java code you would write this as:

```java
("mvn" + "git").replaceAll("(.)", "$1a")
=> "mavanagaiata"
```

## Contribute

Mavanagaiata is an open-source project. Therefore you are free to help
improving it. There are several ways of contributing to Mavanagaiata's
development:

* Build projects using it and spread the word.
* Report problems and request features using the [issue tracker][2].
* Write patches yourself to fix bugs and implement new functionality.
* Create a Mavanagaiata fork on [GitHub][1] and start hacking. Extra points for
  using GitHub's pull requests and feature branches.

## License

This code is free software; you can redistribute it and/or modify it under the
terms of the new BSD License. A copy of this license can be found in the
included LICENSE file.

## Credits

* Sebastian Staudt -- koraktor(at)gmail.com

 [1]: https://github.com/koraktor/mavanagaiata
 [2]: https://github.com/koraktor/mavanagaiata/issues
