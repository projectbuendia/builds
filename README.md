# Project Buendia build repo
This repo makes Project Buendia builds available at [projectbuendia.org/builds](http://projectbuendia.org/builds).

In particular, it hosts the Debian package server that can be used to install the Project Buendia
packages at http://projectbuendia.org/builds/packages.

To add this repository to your Debian-based distribution, use something like:

```sh
echo "deb [arch=all] http://projectbuendia.org/builds/packages stable main" \
> /etc/apt/sources.list.d/buendia-base.list
```

Note that this is hosted on Github Pages, so you won't be able to rely upon directory listings to
browse the repository.

## How new builds are added

Every time [our Travis CI project](https://travis-ci.org/projectbuendia/buendia) runs on either the
`dev` or `master` branches, a new build is pushed to this debian repo. This should make it available
to existing servers for upgrade immediately.

## Some performance caveats to be aware of

Note that there's a real chance that our CI run times will blow out significantly as a result of
cloning this repo, which is full of binary files. If / when this happens, a good solution is to:

- Clone the repo locally
- Delete the `packages` folder
- Push the repo
- Kick off a new build.

Admittedly, this isn't a sustainable solution - if you have any other ideas - especially around how to only take a small number of previous builds - please take a look at
https://github.com/projectbuendia/buendia/blob/dev/.travis.yml and send a pull request :)
