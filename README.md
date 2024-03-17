# Cesar Guzman Website

This repository can be found under [cguz.github.io][website].

## Structure
This repository has a specific folder, file and branch setup which are important if you want to PR changes to us.

### Branches
The repository has two specific branches: `development` and `master`.

`development` is the default branch and should always be targeted for Pull requests when you make changes to it.  
Every change made in the `site` directory will be transferred to the `master` branch to be handled.

`master` should **never** be manually edited. It is the branch used by GitHub Pages to actually publish the website and contains all required files to do so.

### Folders and files
There are many folders and files in this repository that all serve a different purpose.

#### `.github/workflows`
Contains the workflow used to push changes from `development`'s `site` directory over to the `master` branch for publishing.

#### `site`
Contains additional folders and files used for the actual website.  
Everything uploaded and edited in here will be transferred to the `master` branch and as a result published to GitHub Pages.

Here are a few more details and specifics about the folders:

- `_data`  
  Contains the `navigation.yml` which is used for setting up the different navigations on the website.
- `_includes`  
  Used to store overrides of the Minimal Mistakes theme and also some additional header/footer HTML code.

In addition to these folders does the `site` directory also contain a `Gemfile`, which is used for managing Ruby and Jekyll dependencies and the `_config.yml` which is the main file for changing Settings of both Jekyll and the Minimal Mistakes theme.

## License
The content of this repository - and by extension the Website itself - is licensed under the `GNU AGPL-v3.0` License.  
Please read the [LICENSE] file for more details.

## Credits
Special thanks and credits go to the following groups and people:

- The [Jekyll Team][jekyll-team] for making and maintaining [Jekyll]
- [Michael Rose][mmistakes] for the [Minimal Mistakes][minimal-mistakes] theme
- The awesome people of [GitHub] for their [GitHub Pages][pages] service
