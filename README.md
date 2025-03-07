# Hosting A Static Website on GitHub

## About

**Purpose**:
This README describes the process of generating a static website then hosting it on a forge. The specific tools chosen are Markdown for the website's contents, [Pelican](https://getpelican.com/) (static site generator), and [GitHub](https://github.com/) (forge).

This README is suitable for people with a basic level of technical knowledge who wants to host a simple website. This README is also suitable for people who would like to learn documentation practices and tools as it contains relevant information from *Modern Technical Writing* by Andrew Etter.

> Information from Andrew Etter appear in quock blocks like this.

**Definitions**
- **markdown**: a light-weight readable markup language.
- [static site generator](https://en.wikipedia.org/wiki/Static_site_generator): convert local documents into HTML web pages.
- [forge](https://en.wikipedia.org/wiki/Forge_(software)): web based platforms for collaborative developing software projects, some have website hosting capabilities.

## Prerequisites

**You will need:**
- a resume in markdown format
- an email (to sign up for GitHub).
- a computer/laptop/similar device.
- a web browser.
- internet access.

**You should know how to**:
- write basic Markdown.
- perform simple operations on the command-line (e.g. change directory, run command).

## Instructions

### Prepare the Resume

> XML and HTML are hard to write and hard to read. Lightweight markup languages (e.g. Markdown) are easy to write, maintain, and readable in its raw form.

1) Open the resume file.
2) Add metadata to help Pelican generate the website.
	1) Add `Title: Your Name` (e.g. "Title: Jane Doe") as the first line of the resume.
	2) Add `save_as: index.html` as the second line of the resume to make it the home page of the website.
	3) note: these metadata fields and text will not appear on the website.
3) Save the file.

### Static Site Generation

> Build websites rather than pdfs because websites can be updated, fixed, and kept in sync with the latest changes.

#### Initialize Pelican

> Static websites are fast, simple, no dependencies to servers and databases, portable, secure, allows local testing, and cannot crash.

1) Download [Pelican](https://getpelican.com/) by following the instructions on the website.
2) Create a folder to hold the source files for the website. This folder will hereon be referred to as the “source folder".
3) Navigate to the source folder on the terminal.
4) Run command `pelican-quickstart`.
5) Follow the on-screen prompts.
- note: on success, the source folder will now contain 2 subfolders: `content` and "`output` as well as 2 files: `pelicanconf.py` and `publishconf.py`.

##### Sample Quick Start Options

1) Where do you want to create your new website?  `C:\Users\JaneD\sourceFolder`
2) What will be the title of this website `Jane Doe's Resume`
3) Who will be the author of this website `Jane Doe`
4) What will be the default language of this web site? `EN`
5) Do you want to specify a URL prefix? `n`
6) Do you want to enable article pagination? `n`
7) What is your time zone? \[Europe/Rome\]`Europe/Rome`
	- note: see [List of Database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) .
8)  Do you want to generate a tasks.py/Makefile `n`

#### Set Up The Website for Pelican

1) Create a new subfolder named "pages" under the content subfolder.
2) Put the resume Markdown file in the pages folder.
	- note: the resume file has path `source/content/pages/resume.md`.
3) (optional) Open `pelicanconf.py` to simplify website content so it contains only the resume.
	1) Delete section `LINKS = (...)`.
	2) Delete section `SOCIAL = (...)`.
	3) add line `RELATIVE_URLS = True` to the end of the file.
	4) add line `DISPLAY_PAGES_ON_MENU = False` to the end of the file.
	- note: the `pelicanconf.py` file should now look like this:
	- ![pelican configuration](assets/pelican-conf.png)

#### Generate the Website

1) Go to the source folder on the terminal.
2) Run command `pelican content -s pelicanconf.py`.
- note: output on success: `Done: Processed 0 articles, 0 drafts, 0 hidden articles, 1 page, 0 hidden pages and 0 draft pages in <x> seconds.`
-  note: the file `source/output/index.html` will hereon be referred to as the "website file".

#### Preview the Generated Website

1) Go to the source folder on the command line
2) Run `pelican --listen`
3) Go to `127.0.0.1:8000` on the browser
4) note: On success, the resume should appear as a website.
5) End the preview by pressing `Ctrl-D` on the keyboard.

### Hosting Websites on GitHub

> Distributed version control systems "have better performance, allow for offline work, and are superior for concurrent work on the same file."

> For technical documentation, storing documentation in the same repository as its corresponding product source code allows the two to stay in sync and also encourage developers to contribute.

#### GitHub Preparation

1) Go to [GitHub Create Account](https://github.com/signup) and follow the instructions to create a GitHub account.
    - note: The free plan is sufficient to host a website.
2) Sign in to [GitHub](https://github.com/).
3) Create a new repository by clicking the `+` button on the top right then selecting "New repository". 
	- ![create repository button](assets/create_repo.png)
4) Enter the repository name (e.g. "resume") in all lowercase, separate words by `-`.
5) Select "Public".
	- note: the page should now look like this.
	- ![new repository fields](assets/create_repo_2.png)
1) Click on "Create repository".

#### Upload the Static Website to the Repository

1) Navigate to the repository on the browser.
	 - note: the repository url will be in the format of `https:github.com/username/repo-name`.
2) Upload all files in the output folder to the repository.
	- optional: for the example, only uploading the `index.html` file and the `themes` folder is sufficient, as it is a single webpage.
3) Describe the changes made in the "Commit Changes" field (e.g. Add resume website files).
- note: the screen should now look like this.
- ![upload files](assets/upload-files.png)
1) Click on "Commit changes".![alt text](image-1.png)

#### Host the Website

1) Go to repository Settings on the top bar 
	- ![repo settings](assets/repo-settings.png)
2) Select "Pages" on the left sidebar 
	- ![page side bar](assets/page-sidebar.png)
3) Under "Build and Deployment>Source", select "Deploy from a branch"
4) Under "Build and Deployment>Branch", select "main" and "/(root)"
	- note: the page should look like this 
	- ![page settings](assets/page-settings.png)
1) Click "Save" to start hosting the website. It may take a couple of minutes.
2) View the website at `https://username.github.io/repo-name`

#### Make Changes To The Website

> Most of the time, version control systems are overkills for documentation writers. However it's still useful to know how they work and use them since the developers use them.

1) Edit the resume (under `content/pages`) as needed.
2) Regenerate the website file.
	1) Go to the source folder on the terminal.
	2) Run command `pelican content -s pelicanconf.py`.
3) Update the website file on GitHub.
	1) Copy the contents of `output/index.html`
	2) Open `index.html` on GitHub in edit mode.
	3) Replace GitHub's `index.html` contents with the new version (e.g. select-all then paste).
	4) note: this is an inefficient method. However, it is simple to learn, does not require additional resources, and is sufficient for our purposes.
	5) note: see [GitHub Version Control](https://github.com/resources/articles/software-development/what-is-version-control)for the efficient method.
4) Describe the changes made in the "Commit Changes" field (e.g. "Add Skills section").
5) Click on "Commit changes".

## FAQ

**Q: Why use Markdown over other lightweight markup languages?**  
A: Markdown have a clean syntax and is the most popular markup language, which means it have a lot of tools and software support. Andrew Etter is "quite confident that the next great documentation site generator will use a flavor of Markdown"

**Q: Why doesn't updating the markdown file automatically update the website?**  
A: The website's contents is based on the `index.html` file on GitHub. The `index.html` file on GitHub is *updated* by the user. Its contents are *generated* by Pelican based on what's in the content folder. The generation and update to GitHub part is done by the user and are not automatic.

## Resources

[Pelican Themes](https://github.com/getpelican/pelican-themes): customize appearance of webpages

[Common Mark](https://commonmark.org/help/): quick Markdown tutorial

[Markdown Guide](https://www.markdownguide.org/): detailed Markdown information

[GitHub Version Control](https://github.com/resources/articles/software-development/what-is-version-control): efficiently update local changes to GitHub and control history of files.

[*Modern Technical Writing* by Andrew Etter](https://www.amazon.ca/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS): more documentation practices, tips, and tools.

## Contributions

**Group Members**: Carsen Cote, Daniyal Chaudry

**Technology Used**: Markdown, Pelican, Pelican default theme, GitHub, GitHub Pages

**Sources**: In Class Lectures, *Modern Technical Writing* by Andrew Etter.
