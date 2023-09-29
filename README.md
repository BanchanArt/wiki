# BanchanArt Wiki

## About
This is the readme for [BanchanArt / wiki](https://github.com/BanchanArt/wiki), which is the Github repository for the [wiki](https://github.com/BanchanArt/banchan/wiki)
 of the [BanchanArt / banchan](https://github.com/BanchanArt/banchan) repository.

Github Wikis automatically present all .md files, which means you may be viewing this from the repo or from the live wiki itself.

### Details
The default origin of this wiki is `https://github.com/BanchanArt/banchan.wiki.git`. 
Due to this, I have set up a remote known as Github via `git remote add github https://github.com/BanchanArt/wiki.git`.

There a two branches:
- `master`: currently the Github wiki [breaks when trying to rename the branch from master to main](https://github.com/orgs/community/discussions/48537), which is the only reason this still exists
- `main`: created this for pushing updates to github remote

### Process
- While on main, push to github with `git push github main`.
- When ready to merge changes to the live wiki, switch to `master`, merge via `git merge main`, and run `git push origin master`.

### Editing Notes
The Markdown used in [Github Wikis](https://docs.github.com/en/communities/documenting-your-project-with-wikis/editing-wiki-content) differs from the Markdown used in Github Repos. Github Repos use [GFM, GitHub Flavored Markdown Spec](https://github.github.com/gfm/). Github Wikis use [GitHub Markup](https://github.com/github/markup) but is missing some of the features listed in the markup flavors listed there. For instance, wiki files with `.md` ending should be compiled using CommonMarker, but the footnotes extension is disabled whereas the superscript extension works.

Quick Reference Table for Feature Support
| Markdown Feature | Github Wikis | Github Repos | Details |
| :----------- | :------------: | :------------: | ------------: |
|  Notes & Warnings  |   Known Issue   |    Works | Issue opened for this.|
|   Footnotes   |    Not supported, but has a known workaround|      Works | Workaround uses superscript and links. |
|   MediaWiki syntax links   |    Works    |      Does not Work | Best to avoid in README.md|

### Quicklinks
| [BanchanArt / banchan](https://github.com/BanchanArt/banchan) (project repo) |
[Live Wiki](https://github.com/BanchanArt/banchan/wiki) (actual wiki) |
 [BanchanArt / wiki](https://github.com/BanchanArt/wiki) (repo for wiki) |

## Wiki Table of Contents
The following ToC is copied from the [_Sidebar.md file](_Sidebar.md).

-   [Home](Home.md)
-   [Getting Started](Getting-Started.md)
-   [Application Notes](Application-Notes.md)
-   [Environment Variables](Environment-Variables.md)
-   [Operations](Operations.md)

## Useful Links

-   [README](/BanchanArt/banchan/blob/main/README.md)
-   [Code of Conduct](/BanchanArt/banchan/blob/main/CODE_OF_CONDUCT.md)
-   [Contribution Guide](/BanchanArt/banchan/blob/main/CONTRIBUTING.md)

## Additional Links

-   [Banchan Art Website](https://banchan.art)
-   [Security Policy](/BanchanArt/banchan/blob/main/SECURITY.md)
-   [License Information](/BanchanArt/banchan/blob/main/LICENSE.md)

