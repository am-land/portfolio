When I tried to publish my post [*My documentation request form for software features*](https://www.abbymoreland.com/blog/documentation-request-form/), my Netlify build failed. After looking at the deploy log, I immediately knew what went wrong: Netlify didn't have a way to parse the AsciiDoc that my post was written in.

When I deployed my site, I got the following error in Netlify:
```
7:13:16 PM: ERROR 2022/05/11 16:13:16 asciidoctor not found in $PATH: Please install.
7:13:16 PM:                   Leaving AsciiDoc content unrendered.
```
My post is an `ADOC` file, which means it's written in [AsciiDoc](https://docs.asciidoctor.org/asciidoc/latest/document-structure/). To use AsciiDoc with Hugo, you need to convert AsciiDoc to HTML. A straightforward way to do this is to use [Asciidoctor](https://docs.asciidoctor.org/asciidoctor/latest/#what-is-asciidoctor). The Netlify error is telling me that it can't find Asciidoctor, so there's no way for it to publish my AsciiDoc.


### Install Asciidoctor
Make sure Asciidoctor is installed correctly. If you've already installed Asciidoctor in your site's root directory, skip to [Update Netlify's build settings]({{< ref "asciidoc-on-netlify.md#update-netlifys-build-settings" >}}).
> **Before you begin:** Asciidoctor is a Ruby-based processor, so it's packaged as a [RubyGem](https://rubygems.org/gems/asciidoctor). To install Asciidoctor, you'll need to [install Ruby](https://www.ruby-lang.org/en/documentation/installation/).

1. In your site's root directory, run: 
```
$ gem install asciidoctor
```
2. To check that it's the latest version, run:
```
$ asciidoctor --version
```
3. Create a new Gemfile:
```
$ bundle init
```
4. Open your newly created Gemfile and add the `asciidoctor` Gem:

```
source 'https://rubygems.org'
gem 'asciidoctor'
```

5. Save the Gemfile. 
6. In your terminal, install the Gem by running:
```
$ bundle
```

 7. Commit and push your changes.

To upgrade or uninstall Asciidoctor, refer to the [Asciidoctor Docs](https://docs.asciidoctor.org/asciidoctor/latest/install/ruby-packaging/#gem-update).

### Update Netlify's build settings
1. Go to **Site settings** > **Build & deploy** > **Continuous Deployment**.

{{< figure src="1-sitenavigation.PNG" alt="Netlify's site navigation" >}}

2. Under **Build settings**, change **Build command** from **hugo** to **bundle && hugo**.


{{< figure src="2-netlifysettings.PNG" alt="Netlify's build settings" >}}


On your next deploy, this setting will tell Netlify to look for the Asciidoctor Gem in your repo. 

### Troubleshooting

Still getting an error? Here are a few things to check:
- Asciidoctor was installed in your site's root directory.
- Your Gemfile contains only what's listed in this guide and there are no syntax errors.
- Your remote repo contains the `Gemfile` and `Gemfile.lock`.
- Asciidoctor and Hugo are on the latest version.

If your AsciiDoc works locally, it's most likely that Netlify can't find Asciidoctor. The way I discovered my issue and found a resolution was by searching [Netlify's support forums](https://answers.netlify.com/c/netlify-support/support-guides/52) and reading their docs on [Ruby dependencies](https://docs.netlify.com/configure-builds/manage-dependencies/#ruby-dependencies). 


