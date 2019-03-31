![CSCounterBadge](https://img.shields.io/badge/Cheat_sheets_available-60-orange.svg)
![LicenseBadge](https://img.shields.io/badge/License-C_C-blue.svg)
[![PushAndPullRequestIntegrityCheck](https://travis-ci.org/OWASP/CheatSheetSeries.svg?branch=master)](https://travis-ci.org/OWASP/CheatSheetSeries)
[![OfflineWebsiteNightBuild](https://circleci.com/gh/OWASP/CheatSheetSeries.svg?style=svg)](https://circleci.com/gh/OWASP/CheatSheetSeries)

![LogoOfficial](https://github.com/OWASP/owasp-swag/raw/master/projects/cheat-sheet-series/owasp-1.png)

# Welcome to OWASP Cheat Sheet Series V2

This repository contains all the cheat sheets of the project and represent the V2 of the [OWASP Cheat Sheet Series](https://www.owasp.org/index.php/OWASP_Cheat_Sheet_Series) project.

# Table of Contents

- [Cheat Sheets index](#cheat-sheets-index)
- [Special thanks](#special-thanks)
- [Editor & validation policy](#editor--validation-policy)
- [Conversion rules](#conversion-rules)
- [How to setup my contributor environment?](#how-to-setup-my-contributor-environment)
- [How to contribute?](#how-to-contribute)
- [Offline website](#offline-website)
- [Project leaders](#project-leaders)
- [Core technical review team](#core-technical-review-team)
- [Project logo](#project-logo)
- [Folders](#folders)
- [License](#license)
- [Code of conduct](CODE_OF_CONDUCT.md)

# Cheat Sheets index

The following indexes are provided:
* This [index](Index.md) reference all released cheat sheets sorted alphabetically.
    * This index is automatically generated by this [script](scripts/Update_CheatSheets_Index.py).
* This [index](IndexASVS.md) reference all released cheat sheets using the [OWASP ASVS](https://www.owasp.org/index.phpCategory:OWASP_Application_Security_Verification_Standard_Project) project as reading source.
    * This index is manually managed in order to allow contribution along custom content.

You can also search into this repository using a keywords via this URL:

```text
https://github.com/OWASP/CheatSheetSeries/search?q=[KEYWORDS]
```

Example:

```text
https://github.com/OWASP/CheatSheetSeries/search?q=csrf
```

More information about the GitHub search feature can be found [here](https://help.github.com/en/articles/about-searching-on-github).

# Project leaders

* [Dominique Righetto](https://github.com/righettod).
* [Jim Manico](https://github.com/jmanico).

# Core technical review team

**Any GitHub member is free to add a comment on any Proposal (issue) or PR.**

However, we have created an official core technical review team in order to:
* Review all PR/Proposal in a consistent/regular way using [GitHub's review feature](https://help.github.com/en/articles/reviewing-proposed-changes-in-a-pull-request).
* Extend the field of technologies known by the review team.
* Allow several technical opinions on a Proposal/PR, all exchanges are public because we use the GitHub comment feature.

Decision of the core technical review team have the same weight than the projet leaders, so, if a reviewer reject a PR (*rejection must be technically documented and explained*) then project leaders will apply the global decision.

Members:
* [ThunderSon](https://github.com/ThunderSon).
* [Jakub Maćkowski](https://github.com/mackowski).
* [Dominique Righetto](https://github.com/righettod).
* [Jim Manico](https://github.com/jmanico).

# Project logo

Project's official logo files are hosted [here](https://github.com/OWASP/owasp-swag/tree/master/projects/cheat-sheet-series).

# Folders

**cheatsheets_excluded**:
* Contains the cheat sheets markdown files converted with PANDOC and for which a discussion must be made in order to decide if we include them into the V2 of the project due to the content has not been updated since a long time or is not relevant anymore. See this [open discussion](https://github.com/OWASP/CheatSheetSeries/issues/13). 

**cheatsheets_draft**: 
* Contains the cheat sheets files under work by core commiters of the project to facilitate incremental exchanges about the content (PR usage not possible for core commiters).
* Any `.md` file present into this folder is considered **draft** and under heavy work (don't use them for production).

**cheatsheets**: 
* Contains the final cheat sheets files. 
* Any `.md` file present into this folder is considered released.

**assets**: 
* Contains the assets used by the cheat sheets (images, pdf, zip...).
    * Naming convention is `[CHEAT_CHEET_MARKDOWN_FILE_NAME]_[IDENTIFIER].[EXTENSION]`
    * Use `PNG` format for the images.

**scripts**:
* Contains all the utility scripts used to operate the project (markdown linter audit, dead link identification...).    

**templates**:
* Contains templates used for different kinds of files (cheatsheet...).

**.github**:
* Contains materials used to configure different behaviors of GitHub.

**.circleci** / **.travis.yml** (file):
* Contains the definition of the integration jobs used to control the integrity and consistency of the whole project:
    * **[TravisCI](https://travis-ci.org/OWASP/CheatSheetSeries)** is used to perform build and check actions at each Push or on each Pull Request.
    * **[CircleCI](https://circleci.com/gh/OWASP/CheatSheetSeries)** is used to perform regular scheduled build and check actions (night build).

# Offline website

Unfortunately, a PDF file generation is not possible because the content is cut in some cheat sheets like for example the abuse case one.

However, to propose the possibility the consult, in a full offline mode, the collection of all cheat sheets, a script to generate a offline site using [GitBook](https://toolchain.gitbook.com/) has been created. The script is [here](scripts/Generate_Site.sh).

* **book.json**: Gitbook configuration file.
* **Preface.md**: Project preface description applied on the generated site.

## Automated night build

This [link](https://circleci.com/api/v1.1/project/github/OWASP/CheatSheetSeries/latest/artifacts) provide the **url** where to download a night build of the offline website:

```json
[ {
  "path" : "OfflineWebsite-NightBuild.zip",
  "pretty_path" : "OfflineWebsite-NightBuild.zip",
  "node_index" : 0,
  "url" : "https://14-162723104-gh.circle-artifacts.com/0/OfflineWebsite-NightBuild.zip"
} ]
```

The attribute **url** must be used to download the ZIP archive.

## Manual build

Use the commands below to generate the site:

```bash
# Your python version must be >= 3.5
$ python --version
Python 3.5.3
# Dependencies:
#  sudo apt install -y nodejs
#  sudo npm install gitbook-cli -g
$ cd scripts
$ bash Generate_Site.sh
Generate a offline portable website with all the cheat sheets...
Step 1/5: Init work folder.
Step 2/5: Generate the summary markdown page.
Index updated.
Summary markdown page generated.
Step 3/5: Create the expected GitBook folder structure.
Step 4/5: Generate the site.
info: found 45 pages
info: found 86 asset files
info: >> generation finished with success in 14.2s !
Step 5/5: Cleanup.
Generation finished to the folder: ../generated/site
$ cd ../generated/site/
$ ls -l
drwxr-xr-x 1 Feb  3 11:05 assets
drwxr-xr-x 1 Feb  3 11:05 cheatsheets
drwxr-xr-x 1 Feb  3 11:05 gitbook
-rw-r--r-- 1 Feb  3 11:05 index.html
-rw-r--r-- 1 Feb  3 11:05 search_index.json
```

# Conversion rules

* Use the markdown syntax described in this [guide](https://guides.github.com/features/mastering-markdown/).
* Use this [sheet](https://gist.github.com/molomby/9bc092e4a125f529ae362de7e46e8176) for Superscript and Subscript characters.
* Use this [sheet](https://meta.askubuntu.com/a/7383) for Arrows (left, right, top, down) characters.
* Store all assets in the **assets** folder and use the following syntax:
    * `![ALTERNATE_NAME](../assets/ASSET_NAME.png)` for the insertion of an image. Use `PNG` format for the images (this [software](https://www.gimp.org/downloads/) can be used to handle format conversion).
    * `[ALTERNATE_NAME](../assets/ASSET_NAME.EXT)` for the insertion of other kinds of media (pdf, zip...).
* Use ATX style (`#` syntax) for section head. 
* Use `**bold**` syntax for **bold** text.
* Use `*italic*` syntax for *italic* text.
* Use `TAB` for nested lists and not spaces.
* Use [code fencing syntax along syntax highlighting](https://help.github.com/articles/creating-and-highlighting-code-blocks/) for code snippet (prevent when possible horizontal scrollbar).
* If you use `{{` or `}}` pattern in code fencing then add a space between the both curly braces (ex: `{ {`) otherwise it break GitBook generation process.
* Same remark about the cheat sheet file name, only the following syntax is allowed: `[a-zA-Z_]+`.
* No HTML code is allowed, only markdown syntax is allowed!
* Use this [site](https://www.tablesgenerator.com/markdown_tables) for generation of tables.
* Use a single new line between a section head and the beginning of its content.

# Editor & validation policy

[Visual Studio Code](https://code.visualstudio.com/) is used for the work on the markdown files. It is also used for the work on the scripts.

The file **Project.code-workspace** is the workspace file in order to open the project in VSCode.

The following [plugin](https://github.com/DavidAnson/vscode-markdownlint) is used to validate the markdown content.

The file **.markdownlint.json** define the central validation policy applied at VSCode (IDE) and TravisCI (CI) levels.

Details about rules is [here](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md).

The file **.markdownlinkcheck.json** define the configuration used to validate using this [tool](https://github.com/tcort/markdown-link-check), at TravisCI level, all web and relatives links used in cheat sheets.

# How to setup my contributor environment?

See [here](CONTRIBUTING.md#how-to-setup-my-contributor-environment).

# How to contribute?

See [here](CONTRIBUTING.md#how-to-contribute).

# Special thanks

A special thanks you to the following peoples for the help provided during the migration:

- [ThunderSon](https://github.com/ThunderSon): Deeply help about updating the OWASP wiki links for all the migrated cheat sheets.
- [mackowski](https://github.com/mackowski): Deeply help about updating the OWASP wiki links for all the migrated cheat sheets.

# License

See [here](LICENSE.md).
