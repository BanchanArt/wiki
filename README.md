# BanchanArt Wiki

## About
This is the readme for [the Github repo BanchanArt/wiki](https://github.com/BanchanArt/wiki) of the [wiki](https://github.com/BanchanArt/banchan/wiki)
 of the [BanchanArt/banchan Repo](https://github.com/BanchanArt/banchan). 

## Details
The default origin of this wiki is `https://github.com/BanchanArt/banchan.wiki.git`. 
Due to this, I have set up a remote known as Github via `git remote add github https://github.com/BanchanArt/wiki.git`.

There a two branches:
- `master`: currently the Github wiki [breaks when trying to rename the branch from master to main](https://github.com/orgs/community/discussions/48537), which is the only reason this still exists
- `main`: created this for pushing updates to github remote

## Process
- While on main, push to github with `git push github main`.
- When ready to merge changes to the live wiki, switch to `master`, merge via `git merge main`, and run `git push origin master`.


### Quicklinks:
[BanchanArt/banchan Repo](https://github.com/BanchanArt/banchan) |
[Live Wiki](https://github.com/BanchanArt/banchan/wiki)


