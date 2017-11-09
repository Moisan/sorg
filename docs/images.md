# Images

Homebrew:

    brew install graphicsmagick

Documentation:

http://www.graphicsmagick.org/convert.html

## Export input and output paths

    export GMI=~/Pictures/photo-archive/2017-031-portland/L1010468.jpg
    export GMO=.
    export GMO=content/images/passages/001-portland

## Copying paths from finder

Right-click on an image and hold `Option`. The "Copy
<file>" option becomes "Copy <file> as Pathname".

## Resize for article hooks

    gm convert $GMI -resize 75x75^ -gravity center -extent 75x75 -quality 85 $GMO/hook.jpg
    gm convert $GMI -resize 150x150^ -gravity center -extent 150x150 -quality 85 $GMO/hook@2x.jpg

Note the `^` on `-resize` here which treats these numbers
as minimums.

## Resize for article images

    gm convert $GMI -resize 650x -quality 85 $GMO/${$(basename $GMI)/.JPG/.jpg}
    gm convert $GMI -resize 1300x -quality 85 $GMO/${$(basename $GMI)/.JPG/@2x.jpg}

## Resize for fragment vistas

    gm convert $GMI -resize 1024x -quality 85 $GMO/vista.jpg
    gm convert $GMI -resize 2048x -quality 85 $GMO/vista@2x.jpg

## Resize for Twitter cards

    gm convert $GMI -resize 1300x650^ -gravity center -extent 1300x650 -quality 85 $GMO/twitter@2x.jpg

## Resize for Passages images

Landscape:

    gm convert $GMI -resize 1100x -quality 85 $GMO/${$(basename $GMI)/.JPG/@2x.jpg}

Portrait:

    gm convert $GMI -auto-orient -resize 1100x -quality 85 $GMO/${$(basename $GMI)/.JPG/@2x.jpg}

Note we don't bother with a non-retina version because we
can't run Retina.JS.

Note that some systems like Mac OS actually understanding
the `@2x` suffix and will treat the image correctly.

## Identify

Look at EXIF information with:

    identify -verbose <file>
