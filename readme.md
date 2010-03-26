# firin
## overview

firin is a project manager that is designed to "just work". Therefore, it is databaseless. Just put your projects in `$PROJECT_DIR/all` (by default, that would be `~/Projects/all`), and Firin will automatically recognize them.

from the start, firin will work together nicely with git, mercurial, and subversion.

## tags

firin, at its core, uses 'tags'. Tags are just directories filled with symlinks to the actual projects in `all`. A typical structure looks like this:

    $PROJECT_DIR
      |- all
      |  |- shoes
      |  |- coffeescript
      |  |- firin
      |- community
      |  |- shoes        => $PROJECT_DIR/all/shoes
      |  |- coffeescript => $PROJECT_DIR/all/coffeescript
      |- sync
      |  |- shoes        => $PROJECT_DIR/all/shoes
      |  |- coffeescript => $PROJECT_DIR/all/coffeescript
      |  |- firin        => $PROJECT_DIR/all/firin

## syncing

A nifty feature of firin's is the ability to sync your projects automatically from upstream. This can then be scheduled, if you so wish. You can even concurrently sync multiple projects to speed things up with the `sync:concurrent processes (number)` in $PROJECT_DIR/.firin.conf. Use like so:

    firin sync [selector]

Speaking of which, what exactly are 'selectors'?

## selectors

Any command that has a 'selector' argument is asking for you to input a specific group of projects you would like firin to act upon. The format is somewhat like this:

    [project|tag],[project|tag],[project|tag][+,^,!][project|tag],[project|tag]...

Examples:

    firin sync community+sync # syncs every project with the tags 'community' and 'sync'
    firin sync community^sync # syncs every project that includes either tag 'community' or 'sync'
    firin sync sync!shoes     # syncs every project with the 'sync' tag, except 'shoes'.
    firin sync all            # syncs everything

## time management

If you're like me, chances are, you're working on a ton of things at one time. Because of that, you often are overwhelmed and have no idea what to do. Fortunately, firin works with ditz and GitHub's issues. With this powerful pairing, deciding what to do is as simple as:

    firin what-to-do

firin will then look through your projects, querying ditz and gh-issues, and find you a bug/feature request to work on at random. You will never be bored again! (er, hopefully)

## notes

1. a tag must not have the same name as a project, or vice versa. (for hopefully obvious reasons)
2. if a project uses a supported scm (git, hg, svn), firin will automatically attempt to sync it. if you aren't using a supported scm, no scm at all, or want to sync from multiple remotes, you may add a .sync script (must be executable) to the root of each project. example: <pre><code>#!/bin/sh
git pull timmcd master
git pull micah master
git push origin master
</code></pre>
