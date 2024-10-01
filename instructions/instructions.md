# Instructions

## Background

This website is built with [Jekyll](https://en.wikipedia.org/wiki/Jekyll_(software)). It's a basic static site generator and 
content management system (CMS) that integrates nicely with GitHub.
Jekyll makes use of [Markdown](https://en.wikipedia.org/wiki/Markdown) as the basis for most of its content generation. 
Keeping in mind that it's a website, so everything fundamentally gets transpiled/compiled into HTML, Javascript and CSS - but these details do not need to be known.
Markdown is the same as the "Markdown" part in _R Markdown_, and a similar idea to LaTeX (in fact, this instruction manual was written in Markdown).
Where Markdown is limited, one is able to either create custom templates or insert plain HTML/JS in order to achieve their desired outcome.

The Jekyll template chosen here is based on [Long Haul](https://github.com/brianmaierjr/long-haul). It's had a number of further adjustments
and improvements.
Note that each template have different limitations so not all Jekyll websites can follow the exact same set of instructions.


## Structure

The basic structure for simple editing exists in the root directory, starting with `_config.yml`. This is the basis for the 
structure of the website. It dictates the pages displayed as well as other details of the website such as meta descriptions etc.

Next, there are the pages themselves, these are the Markdown files, with the file extension: `.md` (`index.md`, `our-team.md` etc.). Here you will find the content for the website. 

Note that there are other files and directories but most will not need to be touched - they exist for the setup of the page. 
- `_layouts` include the custom templates made. `_includes` consist of the minimal parts/elements that construct the page.
- `assets` contains the images and other content such as favicons (this will be added to if more images or data is added).

## How to edit

Please first familiarise yourself with these two pages which are key to making successful edits of the website:

- Markdown syntax (necessary for the aforementioned `.md` files): https://www.markdownguide.org/basic-syntax/
- YAML (less necessary but needed for the aforementioned `_config.yml` file): https://spacelift.io/blog/yaml

There is plenty of additional unnecessary information that may not be needed in the above links, but it's worth providing a single spot for guides on each.

**The majority of updating this website will be copying the pre-existing formatting in these files.** Please familiarise yourself with the pre-existing files
(namely the ones in the root directory suffixed with `.md` and `_config.yml`).

If a new page is needed duplicate (and rename) an existing file (such as `our-team.md`) and then under the `navigation` key 
in `_config.yml` add the file/path (excluding the file extension `.md`).

Once you make a git `commit` all that needs to be done is a `push` and the rest is handled from there by GitHub pipelines.

### Layouts and Custom Templates

1. Each page starts with an enclosing `---` (3 dashes), this is called [front matter](https://jekyllrb.com/docs/front-matter/).
It's a small section that sets up the page. In this template it's quite simple. Leave `layout: default` but change the `title` 
based on what the new page is - this dictates the name of the page that shows in the tab of your browser.

As for the rest of the page it's in standard markdown - so edit as per usual. 

##### Custom layouts/templates worth mentioning:

1. The page `our-team` has the tables wrapped like so:
    ```html
    <div class="team-table">
    <div markdown="1">
    
    |-------|--------|
    | Table item 1 | Table item 2 |
    | Table item 3 | Table item 4 |
    
    </div>
    </div>
    ```
    
    The outer `div`s are necessary for specific table formatting that relates to the particular table formatting for this page.
    The part enclosed in the div is a Markdown table, its formatting can be seen [here](https://www.markdownguide.org/extended-syntax/) (from the aforementioned Markdown guide)

    Note that the actual table in the file makes use of [Markdown's image linking](https://www.markdownguide.org/basic-syntax/) (again from the aforementioned Markdown guide).
    To add further headshots you would add them into the `assets` folder (`/assets/img/headshots`). 
    It should be noted that before adding more headshots they should be preferably in JPG format and sized to `267 x 300 pixels`.


2. Next worth mentioning is the custom accordions in `research.md`. This is a custom element template (using Liquid tags).
   ```markdown
    {% include_relative _layouts/_elements/accordion.html
        title = "Authors ‘[Link name](link)’ foo"
        content = "_Abstract_: this is the abstract text foo."
    %}
    ```
    This custom template must adhere to the above structure. The only thing that needs to be changed is the bits between the double quotation marks `""`.



## Editing locally

Whilst it is possible to directly edit files in GitHub it's not recommended as you may end up pushing some changes that do 
not generate/render correctly - and this can be seen publicly.
This is why the recommendation is to edit locally first, see the changes before making them public and then push.

### On MAC

Luckily a lot of the Ruby ecosystem is installed on MAC so you should be able to execute the following from the _terminal_.
Don't forget to navigate to the directory the repository is in. Execute the following commands on by one.

### On Windows

Download the latest Ruby from https://rubyinstaller.org/

Then after that has installed execute the following commands one by one in PowerShell. Don't forget to navigate to the directory the repository is in.

#### Commands for both MAC and Windows:
```bash
gem install bundler # may not be necessary

bundle install

bundle exec jekyll serve --force_polling
```

From there a link to the local website should display in the terminal. Place that URL in your browser to review the changes locally.
Continue to make edits and the page should update with those changes. If it doesn't you can cancel the command and rerun it.
Once content with the changes push to the `main` branch and the rest will be handled from there and published to the public website.

Note that for both MAC and Windows once the above setup has been completed for the first time, you will only need 
`bundle exec jekyll serve --force_polling` to view the changes again in the future.
