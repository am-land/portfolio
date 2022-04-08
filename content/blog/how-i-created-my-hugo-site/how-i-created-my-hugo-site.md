---
title: "How I created my Hugo site"
date: 2022-03-30T15:42:45-06:00
ShowReadingTime: true
ShowBreadCrumbs: true
draft: true
---
> Summary: I wanted to build a fully customizable website without starting from scratch, so I created this site using Hugo and Netlify.

Here's how I created my site using a static site generator to host my blog and portfolio.


## Why did I want a website?
I created a customizable website because I wanted to:
- Host my portfolio.
- Contribute to my own blog.
- Create a landing page for my social links.
- Learn how to build, host, and deploy a site for free.
- Develop my knowledge of HTML and CSS.


### My site requirements
At the start of my project, I assessed what I was looking for in a site and came up with a few requirements:

**Static**\
I don’t need a dynamic site because I want to manually update all my content.

**Fast with a simple interface**\
I want a clean, simple site that will load quickly.

**Modern look**\
I don’t need anything fancy, but I don’t want my site to look outdated.

**Low-code but customizable**\
I’m not a web developer, but I am technical and I want the option to fully customize my site.

## CMS or SSG?
Content management systems (CMSs) like WordPress, Drupal, and Squarespace are popular for non-developers because they’re easy to learn and are all-in-one platforms. I’ve been using CMSs since I was a kid making websites for my friends. So, something like WordPress with a WYSIWYG editor was a practical choice. I could create a site, install a theme and some plugins, and publish my content in an afternoon. 

But being part of the [Write the Docs](https://www.writethedocs.org/) community for several years, I knew about static site generators (SSGs). SSGs are applications that create a web server using templates or components and markup files, and compile these files into a site. The site builds and is ready to serve when you deploy it, rather than waiting for someone to request it. This makes it straightforward to update---all data and content are stored in your local directory---and extremely fast, as there’s no database to call. 

As a bonus, there are many open-source SSGs to choose from.


## Jekyll vs Hugo
Though there are SSGs for many programming languages, Jekyll is one of the original SSGs and is still widely used. It’s written in Ruby, so it requires the [Ruby package](https://www.ruby-lang.org/en/downloads/) before you can install it. There are lots of themes available, as well as a large online community with nearly 10,000 forks on GitHub. Popular tech writer [Tom Johnson](https://idratherbewriting.com/) created a [Jekyll documentation theme](https://idratherbewriting.com/documentation-theme-jekyll/).

**Note:** Jekyll does not officially support Windows, but I was able to install it on my 
Windows machine using [Jekyll’s guide](https://jekyllrb.com/docs/installation/windows/). You can also run Jekyll on the Windows 
Subsystem for Linux.

Hugo is another popular SSG, known for its speed and simplicity. It’s written in Go, a compiled programming language originally developed by Google. Hugo also has hundreds of themes, many of them ports from Jekyll themes. Hugo uses its own web server to build and serve the site, so there are no dependencies to get started. Once your site is ready for production, you may want to [publish to a more powerful server](https://openwritings.net/pg/hugo/hugo-deploy-public-folder-local-apache-server) such as [Apache](https://www.apache.org/), though you can keep using the built-in server.

As a documentarian (and an SSG noob), I chose the site generator that came with clearer, more robust documentation. Plus, the Hugo community has grown substantially over the past few years, so I was able to easily troubleshoot issues.

## Getting started

> This guide applies to Windows only. There’s usually more than one way to do something, so make sure to research which methods work best for your stack.
### Prerequisites
Before you begin, you’ll need the following (all open-source):

- [Git Bash](https://gitforwindows.org/) 
- A text editor (I like [Visual Studio Code](https://code.visualstudio.com/))

It’s helpful if you already have:
- Basic knowledge of the [command line](https://www.codecademy.com/article/command-line-commands)
- Knowledge of Git
- Knowledge of Markdown

You’ll also need free accounts for the following:
- [GitHub](https://github.com/)
- [Netlify](https://www.netlify.com/)

### Install Hugo
I installed Hugo on Windows via [Chocolatey](https://chocolatey.org/install) in the terminal. Run PowerShell as an administrator and use the following command:

```
choco install hugo -confirm
```
  
If installed in your root directory, Chocolatey will install Hugo in the following file path: *C:\Users\USERNAME\AppData\Local\Temp\chocolatey*.

> There is an extended version of Hugo that some themes require. Reference the theme’s 
> README to determine what you need.

You can also install Hugo via [other package management tools](https://gohugo.io/getting-started/installing#quick-install) like Homebrew. Or, you can [manually install it](https://gohugo.io/getting-started/installing#windows).

If you want to verify the version, use:

```
hugo version
```

## Create a site
To create a site, use the terminal to navigate to the directory where you want to store your site. It doesn’t need to be in the folder where Hugo was installed. 

Enter the command:

```
hugo new site [name]
```

Replace `[name]` with the name of your site.

If you get an error, make sure Hugo is installed correctly and the PATH variable is set.

### Add a theme
There are many [Hugo themes](https://themes.gohugo.io/) to choose from. I recommend choosing a theme that:
- Includes a demo.
- Has thorough documentation.
- Has been updated within the past two years.

If you’re looking to create a documentation site, [Docsy](https://themes.gohugo.io/themes/docsy/) is popular within the Write the Docs community.

Each Hugo theme is a GitHub repository. There are a few ways to add a theme:

**Method 1:**  
Use Git to clone the repository into the `themes` folder:

```
$ git clone https://github.com/USERNAME/name-of-repo.git
```

Replace the URL with the URL of the theme repo.

**Method 2:**
If you’re using Netlify to deploy, you’ll need to add the theme as a [submodule](https://www.atlassian.com/git/tutorials/git-submodule). In the `themes` folder, use:

```
$ git submodule add https://github.com/USERNAME/name-of-repo.git
```

Replace the URL with the URL of the theme repo.

**Final step:**  
Update the `config.yaml` file to include the name of the theme:

```
theme: “ThemeName”
```

> **Tip:** Here’s a [Git reference sheet](https://training.github.com/downloads/github-git-cheat-sheet/). 

### Serve the site locally
To serve the site locally, enter this command from your site’s directory:

```
hugo server
```

Hugo’s web server watches for changes while it’s running. Whenever you make a change locally, Hugo simultaneously rebuilds and serves the site. Then, LiveReload silently refreshes your browser. To watch the updates as you make them, keep the browser open on a second monitor or on one half of your monitor.

This setup is ideal for beginners because you can instantly see the changes you make. No need to go make a cup of coffee while waiting for your site to build.

## Understanding the Hugo file structure
Running `hugo new site` creates the following directory structure:
```
.  
├── archetypes   
├── content  
├── data  
├── layouts  
├── static  
├── themes
└── config.toml 
```

While it’s important to [learn about each folder](https://gohugo.io/getting-started/directory-structure/), I found it most useful at the start to learn about the config file and the content structure.

**Config file:**  The config file (default `config.toml`) contains the configuration for your site, such as the site title, baseURL, language, theme, and other parameters. The format can be in TOML, YAML, or JSON.

**Content:**  Hugo’s content is made up of markup files called content types. Your Hugo site renders the same structure used to organize your source content. Hugo illustrates this [in their docs](https://gohugo.io/content-management/organization/#organization-of-content-source).

If you create a `new-folder` in the `content` folder, Hugo uses a template to build a **list page** (a page that links out to other pages). If you create a  `new-file` within `new-folder`, Hugo builds a **single page** (for example, this blog post).  

### Content management  
Hugo has thorough documentation on [content management](https://gohugo.io/content-management/) which I recommend reading. For quick reference, here’s a list of what I found helpful as a beginner:

**Front Matter**  
Front matter is metadata embedded within each “content type” or page. For example, the variables you may want for a blog post include: **title**, **author**, **date**, **categories**, **summary**, and **url**. Hugo has predefined front matter variables, but you can also define your own. If you’re using a theme, be sure to reference your theme’s documentation on variables.

The `type` variable determines the *type* of the content; Hugo will derive this from the directory, but you can override it in your front matter.

**Page Bundles and Page Resources**  
*Page bundles* are a way of organizing your content within your file structure. With page bundles, you can group page resources---e.g. images, documents, and other pages---in the same folder so it’s easier to create and update pages. To create a page bundle, add an `_index.md` or `index.md` file within the page’s root directory.

*Page resources* are the files you want to include on a page. They are only accessible from their associated page bundle. 

**Archetypes**  
Archetypes are the templates for your content. They are Markdown files that contain front matter which is used when you create a new content file using that archetype. If a content folder has an associated archetype, new content files you create in that directory will use the archetype. If there’s no archetype for a content folder, Hugo uses the `default` archetype. 

**Shortcodes**  
Shortcodes are snippets inside your Markdown files that call templates. Rather than needing to use HTML tags to embed page resources (e.g. ``<iframe>``), Hugo uses shortcodes. It comes with a lot of [built-in shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugos-built-in-shortcodes), but you can also make custom shortcodes. Mike Dane has a step-by-step tutorial on [Shortcode Templates](https://www.mikedane.com/static-site-generators/hugo/shortcode-templates/) to demonstrate how they work.

## Host and deploy your site

### Host your repository on GitHub
When you’re ready to publish your site, the first step is to create a remote repository (repo) in GitHub for your source code. (You don’t have to use GitHub; in fact, if you’re deploying via Netlify, you can host there too.)

> We won’t be using [GitHub Pages](https://pages.github.com/) in this tutorial, just GitHub itself.

**Step 1:** Follow the steps in [Creating a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) to create a remote repo in GitHub. 

> Tips when creating your repo:
> - Make the repo public.
> - You'll likely want to initialize it *without* a README.md file.
> - You may want to add a license. If you’re unsure about this step, the [Open Source Guide](https://opensource.guide/legal/#which-open-source-license-is-appropriate-for-my-project) is a good place to start.

**Step 2:** Push your code to the GitHub repo you just created:
1. Open your GitHub repo in a browser. 
2. Click the **Code** button and copy the repo’s URL.
3. Run Git Bash as an administrator and navigate to the site directory.
4. Enter this command to connect the remote repo with your local repo:
	```
	$ git remote add origin https://github.com/YOUR-USERNAME/name-of-your-repo
5. Enter `git status` to verify the branch.
6. Then, push your changes from your local repo to your remote repo:
	```
	$ git push -u origin main
	
    ```
    **Note:** `origin` is the `[remote repo name]` and `main` is the `[branch name]`.  

7. Enter `git remote -v` to check if the remote repo was added successfully. 



> If you added your theme as a submodule, don’t forget to also [fork and clone](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop) the theme repo. If you don’t do this step, your GitHub site repo will point to the original theme repo and any changes you make to the theme locally won’t get pushed with the rest of your code.




### Deploy your site on Netlify
I used [Netlify’s guide](https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/) to deploy my site. This guide uses GitHub as the repo source.

Here’s an overview of what you need to do:
1. Once logged in to Netlify, click a button to add a new site from Git.
2. Give Netlify access to your GitHub repo.
3. Select the repo you created for your site.
4. Configure a few settings for your site.
5. In the Netlify UI, click a button to build your site.

Netlify will generate a URL for your site; it should be live at that URL. You can change the name in **Site settings**, though the URL will end in `netlify.app` unless you use a custom domain.

### Host a domain
You can buy a domain name from many sites. I purchased mine years ago from [Google Domains](https://domains.google/) for $12/yr. You can also buy a domain directly through Netlify.

To use your domain with Netlify, follow the steps in [Configure external DNS for a custom domain](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/). Note that updating your domain usually takes up to 24 hours.

## Working with feature branches
If you're the sole contributor to your site, you likely won't need to create a detailed version control strategy. However, it's still a best practice to create feature branches so you won't be making changes directly in your main branch. Instead, you'll make changes to a feature branch and then merge into main. For example, if you're writing a blog post, you can work on it in a branch specifically for adding posts.

There are different conventions for managing and naming branches; you may want to research what makes the most sense for your use case. To create a branch based on main, use Git in your site repo:
```
$ git branch [branch_name]
```
If you're using Visual Studio Code to write posts, you can switch between branches directly in your workspace.

Since you're not creating a pull request that others will review, you likely won't need to resolve any merge conflicts. If you do, Microsoft has a [guide explaining what a merge conflict is](https://docs.microsoft.com/en-us/azure/devops/repos/git/merging?view=azure-devops&tabs=visual-studio-2019).

> If you're interested in learning more about managing branches, Microsoft DevOps has a guide: [Adopting a Git branching strategy](https://docs.microsoft.com/en-us/azure/devops/repos/git/git-branching-guidance?view=azure-devops).


## Troubleshooting tips
No matter how experienced you are, it’s inevitable that you’ll get stuck when learning something new. Whether you get an error, can’t figure something out, or just aren’t sure how to proceed, everyone who works in tech has been there many times.

Here are some tips when you run into issues:

**Stay calm when you get errors or don’t know something.** It's not easy, but staying calm is a crucial skill that will help you solve problems. Midway through creating my site, I got an error message that said I needed to rebuild everything. Instead of getting caught up thinking this was evidence that I didn’t know what I was doing, I took a few deep breaths and told myself I was going to figure it out. I was able to rationally analyze my problem and move forward. I fully believe that staying calm is the key to success.

**Focus on one problem at a time.** It’s common to get overwhelmed by all the things you don’t know. But when you’re learning something new, it’s a trap to follow down every detailed path. Instead, try to stay focused on learning one component until you see the results you expected.

**Google everything.** Google error messages, keywords, possible root causes, or anything that might produce a relevant result. Google the same thing in different ways. It’s highly likely the error you received has a documented solution on Stack Overflow, Reddit, or someone’s blog. If not, [ask Hugo](https://discourse.gohugo.io/).

**Read error messages.** It seems obvious, but sometimes we panic and skim through errors while jumping straight to problem-solving. Take a few seconds to read error messages word-for-word. (Keep in mind, though, that not all error messages are well-written.)

**Take a break.** When you’re struggling with a problem, go grab a beer and focus on something else for a while. Many people solve problems while doing mundane tasks like showering; for me, I nearly always solve my hardest problems while lying awake at night.

For more, read my post The Developer’s Problem-Solving Mindset.

## What I did to facilitate learning
**I contributed to a process log from installation to deployment.**  
This was a single pageless Google Doc that turned into a stream of consciousness as I figured things out. I copied/pasted error messages, linked resources I found helpful, figured out the right questions to ask, added screenshots of the process, documented my steps, and explained each component as I went along.

When I encountered a blocker, I wrote down three possible root causes and troubleshot each one. This process helped me follow the logic in my initial thinking and remember what I had already tried. It also helped me write this post.

I recommend using a process log. It takes more time, but it’s a useful way to learn. Explaining a thing in detail is a great way to solidify your knowledge. 

**If something “magically” happened the right way, I reverted my changes until I understood what I was doing.**  
Sometimes, you press a button or copy/paste unknown code and, magically, that makes something good happen. While this feels like a win, I forced myself to undo changes until I knew what I did to prompt the change. I then tracked in my process log what change I intended to make, what I did to make it, and why it worked.  

**I wrote down the changes I wanted to make but didn’t know how yet.**  
As I customized my theme, I kept a backlog of what I wanted to change later. This kept me from getting sidetracked trying to figure out lots of detailed tasks when it was more efficient to focus on one thing at a time.


## Additional resources
- [Hugo’s Get Started Guides](https://gohugo.io/getting-started/)
- [Mike Dane’s Hugo Videos](https://www.mikedane.com/static-site-generators/hugo/)
- [Ryan Schachte’s Creating a Blog with Hugo and GitHub in 10 minutes](https://www.youtube.com/watch?v=LIFvgrRxdt4)
- [DistroTube’s Building Websites with Hugo](https://www.youtube.com/watch?v=927wgzzNMEA)
- [Regis Philibert’s Hugo Page Resources](https://www.regisphilibert.com/blog/2018/01/hugo-page-resources-and-how-to-use-them/)
- [Docsy’s Best Practices on Content](https://www.docsy.dev/docs/best-practices/)

