# Local Leanpub

We don't need to use Leanpub to render our Leanpub book previews. We can do
that locally using [Pandoc](http://johnmacfarlane.net/pandoc/) and save about
ninety seconds each time.

This repo is an extraction of some work I did to stitch together a local
preview of my book on [Writing With Vim](https://leanpub.com/vim-for-writers).
Here is a way to get your own book previews without the need to send your work
up to Leanpub every time.

The setup in this repo takes care of some of the work of moving files and
normalizing differences between Leanpub and Pandoc so that you can easily and
quickly preview the book contents.

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

## How book contents are laid out

Leanpub looks at certain files to compile the book in question:

 * `Book.txt` lists all of the chapters of the final book
 * `Sample.txt` lists the chapters in the sample PDF

We have a file called `contents.txt` that holds the values of things in the book.

My convention is that the book contents are located in `chapter[digit].markdown`
files. You can always change the scripts if this does not suit you.

## Installing

Clone this repo and put it into your Dropbox folder that Leanpub looks at.
Then you should be able to run the commands above and see a local preview, and
publish to Leanpub and have a preview up there.

## Pandoc vs. Leanpub

Leanpub used to use the Pandoc rendering system, but they switched to use their
own system to have better control over the rendering process. and they support
many of the same conventions. You should still check your book against
Leanpub's preview feature before publishing, since there are some differences.
For example, For example, Leanpub automatically inserts page breaks between chapters
(depending on your settings) while Pandoc needs the explicit `\\pagebreak`
command (this repo takes care of this difference.)

## Disclaimer

This project is not affiliated with Leanpub or Pandoc. It just uses Pandoc to
approximate the preview function of Leanpub.

## License

This code released under the [MIT License](http://en.wikipedia.org/wiki/MIT_License).
