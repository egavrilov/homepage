#Ed: A Minimal Edition Theme for Jekyll

One of our most pressing and ever revolving needs as scholars is to pass on our textual artifacts from one generation to another. The art of textual editing, among other practices, has helped many cultures to remember and interpret for centuries. Alas, that art is practiced and encouraged in its highest form by a dwindling number of scholars. In a digital environment the problem is compounded by the difficulties of the medium. While vast repositories, and "e-publications" appear on the online scene yearly, very few manifest a textual scholar's disciplined attention to detail. In contrast, most textual scholars who have made the leap to a rigorous digital practice have focused on markup, relying on technical teams to deploy and maintain their work. This makes your average scholarly digital edition a very costly, and therefore limited affair. We hope that Ed can help would-be and veteran textual scholars make it easier to deploy their own editions in a lasting way.

Ed is a [Jekyll](https://jekyllrb.com/
) theme designed for textual editors based on [minimal computing principles](http://go-dh.github.io/mincomp/), and focused on legibility, ease and flexibility. In other words, the technology is easier to learn or teach and can produce beautifully rendered scholarly or reading editions of texts. The resulting edition consists of static pages whose rate of decay is substantially lower than database-driven systems. As an added bonus, these static pages require less bandwith.

Here's [the sample site](http://elotroalex.github.io/ed/) built with Ed.

![Sample Ed site](https://github.com/elotroalex/ed/blob/master/assets/screenshot.png)

Ed is built on top of [Lanyon](https://github.com/poole/lanyon), a Jekyll theme based on [Poole](http://getpoole.com), "the Jekyll butler," both created by [Mark Otto](<https://github.com/mdo) and distributed with an MIT license. Thanks to Mark Otto for his helpful streamlining. 

## Features
- Design choices emphasizing a pleasant reading experience of narrative, drama and poetry
- Extensible, minimal structure 
- Responsive and sensible footnote system
- Dublin Core metadata for Zotero recognition to aid in citation
- Ability to generate well-formatted bibliographies using [jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) by [Sylvester Keil](https://github.com/inukshuk/)

## Making an Edition with Ed

- [Installing Ed](#installing-ed)
- [Jekyll](#jekyll)
- [Kramdown and Markdown](#kramdown-and-markdown)
- [Genres](#genres)
- [Kramdown and HTML](#kramdown-and-html)
- [Footnotes](#footnotes)
- [Blockquotes](#blockquotes)
- [Bibliographies](#bibliographies)
- [Tips and Tricks](#tips-and-tricks)
- [Publishing](#publishing)

---

(This documentation was built with beginners in mind, but has the necessary information for more seasoned producers)

## Installing Ed

To install and use Ed you will be using your terminal. If you need a refresher, I highly recommend "[The Command Line Crash Course](http://cli.learncodethehardway.org/book/)" 

N.B. Jekyll does not run very well on Windows machines as of now. If you are using Windows, this theme won't work for you, but we hope that you simply deploy our principles on a system like [Hugo](https://gohugo.io/), which does work on Windows.

The first step to install Ed is to download the source files from Github. To do so you must have git installed in your computer. You probably have git already, but if you don't, here are [some great instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get you started. To make sure git is running on your system enter the following line on your terminal (remember to ignore the $):

~~~ bash
$ git --version
~~~

If you don't get an error, you're good to go. Using the `cd` command on your terminal, navigate to the folder where you keep your web projects. Once you're in the folder where you want Ed to live, download it from github using the following line (remember you can copy and paste):

~~~ bash
$ git clone git@github.com:elotroalex/ed.git
~~~

At this point you should navigate inside your project folder and stay there until further notice:

~~~ bash
$ cd ed
~~~

Jekyll is a Ruby gem (Ruby's name for software packages). Besides Jekyll, Ed needs another  gem to run: jekyll-scholar. I have provided a `Gemfile` that allows you to install the right versions of jekyll and jekyll-scholar. Before you can use this `Gemfile`, you need to setup the right Ruby environment for Ed to run smoothly. The best way to ensure you have the right environment is to use Ruby Version Manager, or [rvm](https://rvm.io/), and the latest stable version of Ruby. To install rvm *and* a recent version of Ruby at the same time, enter the following two lines into your terminal:

~~~ bash
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

$ \curl -sSL https://get.rvm.io | bash -s stable --ruby
~~~

After the process runs succesfully, read the last few lines generated by the terminal. You will see final instructions for making rvm run. Once you finish the process, check to see if rvm is running by entering:

~~~ bash
$ rvm --version
~~~

If you don't get an error, you're ready for the next step. If you do get an error, and don't feel comfortable troubleshooting on the terminal, this is a good opportunity to reach out to a friend who can help. If you're brave enough, the most effective way of troubleshooting in the terminal is to copy and paste the errors into your search engine of choice.

The next step is to create a gemset for your jekyll projects. A gemset is a set of gems. If you don't create and use a gemset, every gem you install will be applied system-wide. This may cause problems down the line, and I recommend against it. To create a gemset:

~~~ bash
$ rvm gemset create edgems
~~~

To use the gemset you just created:

~~~ bash
$ rvm gemset use edgems
~~~

N.B. Everytime you open a new tab on your terminal, you will need to declare the gemset you want to use, or else it will revert to (default).

Now that rvm and Ruby are set up, we're ready to install our first gem: Bundler. Bundler is a gem that allows you to install many gems at the same time using Gemfiles. Once you install it, you will be ready to run the Gemfile I provided in the source files. To install Bundler:

~~~ bash
$ gem install bundler
~~~

If you ran into problems following these instructions, you should try a more detailed walkthrough. Here’s [a great tutorial](https://www.chapterthree.com/blog/ruby-rvm-gemsets-and-bundlergemfiles) on how to do both rvm and Bundler from Rob Decker. 

You're very close. Now that Bundler is installed, the final step is to install the gems we will need to run Ed: jekyll and jekyll-scholar. To do so run the Gemfile this way:

~~~ bash
$ bundle install
~~~

If you don't get any errors, Ed should work at this point. To see if Ed is working properly we will take advantage of Jekyll's built in server. Assuming you're still inside the ed folder, you can now build the first version of your site and run the jekyll server at the same time by entering:

~~~ bash
$ jekyll serve
~~~

Copy the url on your terminal log and paste it into your browser of choice (I recommend Firefox). This url usually looks something like this `http://127.0.0.1:4000/`. At this point you should be looking at your very own working version of Ed:

![Your very own Ed]({{ site.baseurl }}/assets/screenshot.png)

---

## Jekyll

Ed is a Jekyll theme. That means you will need some familiarity with Jekyll to take advantage of its full potential. While running a Jekyll is a bit more involved than Wordpress and other similar tools, the payoff in the long term is worth the effort to learn it. If you are new to Jekyll I recommend you take a look at ["How (and Why) to Generate a Static Website Using Jekyll"](http://chronicle.com/blogs/profhacker/jekyll1/60913) at ProfHacker, and the excellent [Jekyll documentation](http://jekyllrb.com/) to start getting a sense of how it works.

Once you have gone through these tutorials, you can get started using Ed by using the sample texts provided with your own texts. You will probably also want to change the `_config.yml` file to add your own personal information and a site title and description of your choice. to make new texts, simply copy any one of the sample texts as a new file in the `_posts` folder. Remember to always use the jekyll convention for naming posts `yyyy-mm-dd-filename.md`. You should also make sure that all your texts have the YAML front matter (the information at the top of the file). Ex:

~~~ yaml
---
layout: poem
title: "Cahier d'un retour au pays natal"
author: Césaire
---
~~~

---

## Kramdown and Markdown

Ed is designed for scholars and amateur editors who want to produce either a clean reading edition or a scholarly annotated edition of a text. The main language we use to write in the Ed environment is kramdown (a flavor of markdown). To learn more about the Markdown family, see Dennis Tenen and Grant Wythoff's "[Sustainable Authorship in Plain Text using Pandoc and Markdown](http://programminghistorian.org/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown)." Kramdown is convenient for scholars because of the way it handles footnotes. You can become familiar with the kramdown syntax in the [kramdown documentation](http://kramdown.gettalong.org/syntax.html). Another way to become familiar is to examine the sample text source files in your plain text editor. 

---

## Genres

Ed offers three different layouts: poem, narrative and drama. The genre is indicated in the YAML front matter on your texts. Using these layouts will allow you to tweak the stylesheets according to your different needs. Out of the box, Ed contains some special instructions for poetry in it's stylesheets that allow you to deal with some of the peculiarities of poetry layouts.

To indicate lines in poetry we use the line syntax from Kramdown:

~~~ markdown
- Hold fast to dreams
- For if dreams die
- Life is a broken-winged bird
- That cannot fly.
- Hold fast to dreams
- For when dreams go
- Life is a barren field
- Frozen with snow.
~~~

To indent specific lines we take advantage of a feature in kramdown that allows us to indicate classes for a line. This approach still allows the line to be readable while editing. 

~~~ markdown
- {:.indent-3} But O heart! heart! heart!
- {:.indent-4} O the bleeding drops of red,
- {:.indent-5} Where on the deck my Captain lies,
- {:.indent-6} Fallen cold and dead.
~~~

The `-` at the beginning of each line indicates that these are lines. The `{:.indent-3}` is what we need to in order to indicate the indent value for that line. Values can range from 1-10. You can expand the range or adjust the values in the CSS stylesheet in the `public` folder.

The example from Raisin in the Sun shows us that we don't need much special markup for theater as long as we use CAPITAL LETTERS for speakers. Italics for directions are easy enough. Just use `*` around the words you want to italicize. 

The Narrative of the Life of Frederick Douglass shows us an example of narrative that includes footnotes and quoted poetry. See the sections below for how to accomplish these different effects.

---

## Kramdown and HTML

For more hand-crafted layouts---[the title page in *The Narrative of the Life*]({{ site.baseurl }}/toc/narrative.html#title-page), for example---you may choose to work directly with HTML. One of the great advantages of working with Kramdown is that we have a lot of flexibility to mix HTML with the Kramdown syntax. Here is the code for the title page of *The Narrative of the Life*:

~~~ html
<a id="title-page" />
<p class="centered large">NARRATIVE<br>OF THE<br>LIFE<br>OF</p>
<br>
<p class="centered larger">FREDERICK DOUGLASS</p>
<p class="centered large">AN<br>AMERICAN SLAVE.<br>WRITTEN BY HIMSELF.</p>
<br>
<p class="centered">BOSTON</p>
<p class="centered">PUBLISHED AT THE ANTI-SLAVERY OFFICE,<br>NO. 25 CORNHILL<br>1845</p>
<p class="centered small">ENTERED, ACCORDING TO ACT OF CONGRESS,<br>IN THE YEAR 1845<br>BY FREDERICK DOUGLASS,<br>IN THE CLERK'S OFFICE OF THE DISTRICT COURT<br>OF MASSACHUSETTS.</p>
~~~

The effects of this page can be achieved with slightly complex Kramdown, but I chose to use HTML to demonstrate its use and to highlight the presence of size and center classes in the stylesheet. 

A note on line breaks: The use of `<br>` here bears further commenting. In many cases we need to insert and HTML break because Kramdown has the tendency to ignore hard breaks. Feel free to use them whenever you see that the breaks you want are ignored. 

--- 

## Footnotes

Footnotes are the bread and butter of scholarship. Kramdown makes footnotes a fairly simple affair:


~~~ 
- O Captain! my Captain! rise up and hear the bells; 
- Rise up—for you the flag is flung—for you the bugle[^fn2] trills,

...

[^fn2]: The bugle is a small trumpet implicated in the military industrial complex.
~~~

These footnotes can be placed anywhere, but they will always be generated at the bottom of the document. To have a multi-paragraph footnote you need to start the footnote text on the next line after the footnote anchor and indent it:

~~~ 
[^fn3]:
	Ugh pinterest fixie cronut pitchfork beard. Literally deep 
	cold-pressed distillery pabst austin. 

	Typewriter 90's roof party poutine, kickstarter raw 
	denim pabst readymade biodiesel umami chicharrones XOXO. 
~~~

The footnotes system provided by Kramdown does have one limitation. It generates the numeration for you automatically, and it only allows you to have one set of footnotes for a text. In some cases we have to separate the author's footnotes from our own, in others we want to represent the author's own footnote style. In these cases we have to use HTML. Here's the example from *The Narrative of the Life*:

~~~ html
... At this time, Anna,<sup><a href="#fn2" id="ref2">\*</a></sup> my intended wife, came on;

...

<sup id="fn2">[↩](#ref2)</sup> She was free.
~~~

---

## Blockquotes

*The Narrative of the Life* also includes several blockquotes. You can also find another example of blockquote use in the footnote of "O Captain! My Captain!" Simple blockquotes are simple enough in Kramdown:

~~~ 
> This is to certify that I, the undersigned, have given the bearer, my servant, full liberty to go to Baltimore, and spend the Easter holidays.
>
> Written with mine own hand, &c., 1835.  
> WILLIAM HAMILTON,
~~~

To use a line break in block elements add two spaces after the end of the line where you want the break. You can't see them after `&c., 1835.` but they are there.


Things get a bit complicated when we want to use poetry inside the block or when the block is included in another block element, like a footnote. Here's the last two stanzas from A Parody in The Narrative of the Life which shows an example of a blockquote of poetry:

~~~
...
> - Two others oped their iron jaws,
> - And waved their children-stealing paws;
> - There sat their children in gewgaws;
> - By stinting negroes' backs and maws,
> - They kept up heavenly union.
> <br><br>
> - All good from Jack another takes,
> - And entertains their flirts and rakes,
> - Who dress as sleek as glossy snakes,
> - And cram their mouths with sweetened cakes;
> - And this goes down for union.
{:.poem}
~~~

We have two odd pieces of markup in this example. `<br><br>` is needed to separate the stanzas. The `{:.poem}` tells the processor to think of the line aboves as poetry. Because this segment of poetry exists in the 'narrative' layout, we need to signal the processor to process it as poetry.

---

## Bibliographies

To help us style and generate bibliographies and citations, Ed uses the [jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) gem by [Sylvester Keil](https://github.com/inukshuk/). To learn more about how to use the gem, make sure to read the documentation on the link above. 

Pro tip: I recommend you use [Zotero](http://zotero.org/) to keep track of your bibliography for your project. This will make it easy for you to generate the `reference.bib` (a BibLaTeX file) you will need to make jekyll-scholar work with Ed. To export from Zotero in this format all you need is to select the references you need, right click and select `export in...` and choose the BibLaTeX format. Rename your file to reference.bib and move it into the `_bibliography` folder.

Because we are more likely than not to use citations in footnotes or pages that contain footnotes, and because footnotes will be necessarily generated at the bottom of the page, Ed uses a separate page for your Bibliography or works cited. The page is provided for you as a page, and uses the default page layout. Notice that the bibliography itself is generated by a liquid tag:

<pre>
&#123;% bibliography %&#125;
</pre>

If you want your inline citations to link to the bibliography page, instead of writing them by hand, you can use the cite function in jekyll-scholar. In order to point to the bibliography page we need to take advantage of the `--relative` flag in jekyll-scholar:

<pre>
&#123;% cite cesaire_discourse_2001 -r /bibliography.html %&#125;
</pre>

This code generates the citation in [footnote #3]({{ site.baseurl }}/toc/o-captain.html#fn:fn3) in "O Captain! My Captain!." Here's the breakdown:

* `cite` is the jekyllscholar command. 
* `cesaire_discourse_2001` is the unique ID for Césaire's Discours on Colonialism included in the reference.bib file. 
* `-r` is short for `--relative`, a flag signalling jekyll-scholar that we're about to provide it with a relative link path.
* `/bibliography.html`, the relative path of our bibliography.

---

## Tips and Tricks

- The Table of Contents is produced automatically for all texts with the category 'toc'. To create your own table of contents make sure to include the `categories: toc` in your YAML front matter.
- Make sure to add horizontal rules, `---`, to separate sections in your texts. This creates a more pleasant layout.
- You can clean unnecessary from the original Ed package before publishing your site. This will help you reduce overhead. For example, you can erase this page, the sample texts, the `syntax.css` file (used for styling code).
- Consider providing tips for your readers on how to make their font bigger or smaller by taking advantage of <kbd>Command</kbd> <kbd>+</kbd> and <kbd>Command</kbd> <kbd>-</kbd>; or to leverage the power of Google's [site search operator](https://moz.com/blog/25-killer-combos-for-googles-site-operator).
- Ed includes RDF metadata in the headers that makes it easier for users of Zotero to grab bibliographic information for the site and individual texts. The RDF functionality is not enough to generate a full proper citation. Consider providing proper citation information in your about page or homepage.



---

## Publishing

Publishing and Ed edition can be done in one of two ways. You can either host it on a server you rent, own or have access to. Most mortals pay a hosting provider to host their sites. I recommend [Reclaim Hosting](https://reclaimhosting.com/), run by scholars. If you are affiliated with a university, chances are that your institution provides you with a UNIX account and a bit of server space. Since Jekyll generates a full static site for you, that means you can park it there. To do so you need to build the site first. If you have been keeping your eye on your project by using `jekyll serve`, chances are you have a current built site in your project folder labelled `_site`.

If you don't you can build one easily by using the following Jekyll command:

~~~ bash
$ jekyll build
~~~

Using an FTP client like [Filezilla](https://filezilla-project.org/), or [SSH on your terminal](https://www.siteground.com/tutorials/ssh/), you need to push the contents of the `_site` folder to the folder on your server where you would like your project to exist. Depending on your host provider, you may be able to receive help from the sys admins with this step. 

The second option is to publish your site for free on Github Pages. This option can be a bit more complicated than the first because Github is run in `--safe` mode, and will normally reject the jekyll-scholar plugin. We can work around this limitation by generating the site before hand and deploying just the site files. I've provided a useful [Rakefile created by Robert Rawlins](http://blog.sorryapp.com/blogging-with-jekyll/2014/01/31/using-jekyll-plugins-on-github-pages.html) that allows us to do just that. A Rakefile is a series of Ruby commands that can be run at once. More on running this file below.

Whether you decide to publish on Github pages or not, we recommend that you still use git and GitHub to version your edition and make the data available via another channel other than your webpage. This is one of the great advantages of using our system, increasing the chances of survival of your work and opening new audiences for it.

To publish on GitHub pages, you must have a copy of the repository in GitHub. Once you've created the repository that you will use, you must link your local repository to the one on GitHub. Notice that because you cloned the original source files from my repository, it will be linked to my repository (to which you don't have writing privileges) until you do this step. Instructions for changing the remote URL can be found [here](https://help.github.com/articles/changing-a-remote-s-url/).

You also need to create a different git branch called `gh-pages` within your local repository for your site. This is the branch that will get published by GitHub. To create and use that branch use the following command:

~~~ bash
$ git checkout -b gh-pages
~~~

Once you are using that branch, you are ready to publish your site using the Rakefile. To do so use this command:

~~~ bash
$ rake blog:publish
~~~ 

Happy editing!
