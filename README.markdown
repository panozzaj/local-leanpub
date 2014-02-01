# Local Leanpub

We don't need to use Leanpub to render our Leanpub book previews. We can do
that locally using [Pandoc](http://johnmacfarlane.net/pandoc/) and save about
ninety seconds each time.

This repo is an extraction of some work I did to stitch together a local
preview of my book on [Writing With Vim](https://leanpub.com/vim-for-writers).
Here is a way to get your own book previews without the need to send your work
up to Leanpub every time.

This setup takes care of some of the work of moving files and normalizing
differences between Leanpub and Pandoc so that you can easily and quickly
preview the book contents. You can add your own custom steps to the build
process to generate or insert images.

Here is an example (local Pandoc on the right, Leanpub preview on the bottom):

![Pandoc Sample](http://ajp-github.s3.amazonaws.com/pandoc%20sample.png)
![Leanpub Sample](http://ajp-github.s3.amazonaws.com/leanpub%20sample.png)

## Installation

**If you have done any writing, you want to copy this work somewhere so you
don't overwrite it**.

You need to have your book set to file mode (which uses Dropbox) to write in
Markdown locally, which is irreversible (at least at the time of writing.) If
you are writing locally and using Dropbox, you already have this set up. Here
is what it looks like when finished:

![Correct Settings](http://ajp-github.s3.amazonaws.com/correct%20settings.png)

In your Dropbox folder, move the contents of the manuscript folder into a
temporary directory, and then clone this repo. Here is an example:

```
 $ cd $dropbox/mybook
 $ mkdir old_manuscript
 $ mv manuscript/* old_manuscript
   ... look at these directories to make sure everything looks OK
 $ git clone https://github.com/panozzaj/local-leanpub.git manuscript
   ^^^ copies the contents of the repo into the manuscript directory
```

## Local previewing

You need to [have Pandoc installed](http://johnmacfarlane.net/pandoc/installing.html).

At the command-line, run `./build` to generate a PDF locally manually. This
will look at the contents of contents.txt to generate a `Book.txt` file, which
is what Leanpub looks at to stitch together your book correctly.

To automate this process, install the Ruby gems locally with `bundle install`.
Then you can run `bundle exec guard` to automatically regenerate the PDF
whenever the text contents of the book change or you add or remove a chapter
from the book. (For my project, I also use `./build` script to correctly
generate the changes for Leanpub, since I do some post processing to insert
images, etc.)

Open up the `local-preview.pdf` file to see an approximation of what your book
will look like when rendered by Leanpub. Many PDF readers have an auto-refresh
setting, so when your book changes you will see the changes update in the book.

[Optional] after running `./build`, you can confirm that Leanpub can also
understand your project structure by creating a new preview there.

## How book contents are laid out

[Leanpub looks at certain files](https://leanpub.com/help/manual) to compile
your book:

 * `Book.txt` lists all of the chapters of the final book
 * `Sample.txt` lists the chapters in the sample PDF

We have a file called `contents.txt` that holds the values of the raw materials
of the book. `./build` does some post-processing to create new files for Pandoc
and Leanpub to look at. Then it updates `Book.txt` to ensure that Leanpub knows
where to look for the generated files. So if you want to add a new chapter, add
it to `contents.txt` which will be read by `./build`.

My convention is that the book contents are located in
`chapter[digit].markdown` files. I like the `.markdown` extension because it
signals what the contents are and enables syntax highlighting in my text editor
(Vim). You can always change `contents.txt` if this does not suit you.

## Pandoc vs. Leanpub

Leanpub used to use the Pandoc rendering system, but they switched to use their
own system to have better control over the rendering process. They support
many of the same conventions.

You should still check your book against Leanpub's preview feature before
publishing, since there are some differences. For example, Leanpub
automatically inserts page breaks between chapters (depending on your settings)
while Pandoc needs the explicit `\pagebreak` command (the scripts here take
care of this difference.)

## Disclaimer

This project is not affiliated with Leanpub or Pandoc. It just uses Pandoc to
approximate the preview function of Leanpub.

## License

This code released under the [MIT License](http://en.wikipedia.org/wiki/MIT_License).

## Appreciation

If you use this for your book and find it useful, please let me know. It makes
me very happy when someone reaches out! I'd love to know what you are working
on, as well.

Any issues? Please submit an issue / pull request and I'll take a look at it.
