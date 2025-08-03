# installed imagemagick

https://github.com/ImageMagick/ImageMagick/discussions/6294

magick -verbose `G:\-1828-\americandictiona01websrich.pdf` -resize 100% -quality 100 -sharpen 0x1.0 `G:\-1828-\V1-%03d.png`



magick -verbose `G:\-1828-\americandictiona01websrich.pdf` -write `G:\-1828-\V1-%04d.png`

# installed ghostscript

magick -verbose -density 300 .\americandictiona01websrich.pdf .\V1-%04d.png

# 10% CPU, nothing really verbose going on ... not spitting out pages yet ...
# 5:35PM ... cancel, remove density ... 

magick -verbose .\americandictiona01websrich.pdf .\V1-%04d.png
magick -verbose .\americandictiona02websrich.pdf .\V2-%04d.png

# 5:43 start 
# 6:04 very low-res SHIT 
# https://stackoverflow.com/questions/36905337/default-imagemagick-density-when-converting-from-pdf


magick -verbose -density 300 .\americandictiona01websrich.pdf .\V1-%03d.png
magick -verbose -density 300 .\americandictiona02websrich.pdf .\V2-%03d.png
# 6:09 try again ... 6:39 

# try with quality?

magick -verbose -density 600 -quality 100 .\americandictiona01websrich.pdf .\quality-100\V1-%03d.png
magick -verbose -density 600 -quality 100 .\americandictiona02websrich.pdf .\quality-100\V2-%03d.png
# 6:56PM start , 8:28PM spitting out images 


# deskew ... https://stackoverflow.com/questions/41546181/how-to-deskew-a-scanned-text-page-with-imagemagick

magick skewed.png -deskew 80% -set option:deskew:auto-crop true skewed_dec.png
magick skewed.png -deskew 80% skewed_de.png


magick normal.png -deskew 40% normal_de.png

# Mystic/Mystical V2-173, col 2



# find columns 
# find words 
# store x,y bbox for each subimage ... 
# figure out word 
# two words one, entry? will be a bug 
# column entry 0 is if it is from a previous page, entry 1 is the first full word ...

#column 1,2,3
# V2 is 4692x6033, V1 is 2712x3664

# put this in virtualbox debian?  leptonica (c-code) to deskew? 
# or wrap in Python garbage, using computer_vision?

# virtualbox-debian would allow me to use the cleanup scripts of fred ...
http://www.fmwconcepts.com/imagemagick/textcleaner/index.php

# let's do debian with php cli run myClass?

1828 on VPS (namecheap) with Sphinx?  Maybe drop email? mshaffer@mshaffer.com ... 

debian on G: ... move files, or rerun?
setup Guest Addition for bi-directional copy/paste text and files 

Debian 12:::
Debian desktop environment, MATE, web/ssh server, standard system utilities
root and mshaffer 

XML system?
M:\Drive-Q\-lon-\1828d.mshaffer.com

1854 dictionary?
https://archive.org/details/americandictiona00webs_0/page/880/mode/2up
1913 h.s. dictionary.
https://archive.org/details/cu31924031426301/page/632/mode/2up

1913 not available as PDF?
https://archive.org/details/rbanms.webstersrevisedu0000noah/page/2028/mode/2up
https://www.reddit.com/r/dictionary/comments/1m6qxmq/scanned_pdf_of_websters_1913_dictionary/
Webster’s Revised Unabridged Dictionary of the English Language 1913 pdf

# create a dictionary module... 1828 is the default... 

ocr - original / user-input (most voted) / user-input (most-recent) ... e.g., fork the most voted ...
maybe keep the page intact, use css to zoom-in on correct page?  useful with other dictionary values that are nearby (and images overlapping)... zoomed-in css, can zoom out to a two-page system with each element clickable (for thoses that read dictionaries)



