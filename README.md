# Project Buendia build repo

This GitHub repo makes Project Buendia builds available at https://projectbuendia.github.io/builds/.

In particular, it hosts the Debian package repository that can be used to install the Project Buendia
packages at https://projectbuendia.github.io/builds/packages.  (Note that it's hosted on GitHub Pages,
so you won't be able to rely upon directory listings to browse the repository.)

To add this repository to your Debian-based distribution, use something like:

```sh
echo "deb [trusted=yes] https://projectbuendia.github.io/builds/packages unstable main java" \
    > /etc/apt/sources.list.d/buendia-base.list
```

## How new builds are added

Every time [our CircleCI build](https://circleci.com/gh/projectbuendia/buendia) runs on the
`dev` branch, the packages produced by the build are committed and pushed to this GitHub repo.
The contents of this repo are published in [our Debian package repository](https://projectbuendia.github.io/builds/packages) with GitHub pages,
so the new packages will become available to existing servers for upgrade immediately.

## Some performance caveats to be aware of

Note that there's a real chance that our CI run times will blow out significantly as a result of
cloning this repo, which is full of binary files. If / when this happens, a good solution is to:

- Clone the repo locally
- Delete the `packages` folder
- Push the repo
- Kick off a new build

Admittedly, this isn't a sustainable solution. If you have any other ideas, especially around how to only take a small number of previous builds, please take a look at
https://github.com/projectbuendia/buendia/blob/dev/.circleci/config.yml and send a pull request :)
