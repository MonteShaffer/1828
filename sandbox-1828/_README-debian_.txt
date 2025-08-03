# install imagemagick with ghostscript
# debian will be a redo... using mshaffer username ...

# https://linuxcapable.com/how-to-install-imagemagick-on-debian-linux/
sudo apt update && sudo apt upgrade
sudo apt install libpng-dev libjpeg-dev libtiff-dev


sudo apt-get install ghostscript
sudo apt-get install imagemagick

#################



sudo nano /etc/ImageMagick-6/policy.xml
## <policy domain="coder" rights="read|write" pattern="PDF" />
## resource memory|disk to 4GiB
# "convert-im6.q16: cache resources exhausted"
# https://github.com/ImageMagick/ImageMagick/issues/396
## maybe 'comment out' the memory|disk tags ... 


convert --version
# 6.9? we are in convert space, not magick space???

cd /home/mshaffer/Desktop/sandbox-1828/

mkdir quality-100

convert -verbose -density 600 -quality 100 ./americandictiona01websrich.pdf ./quality-100/V1-%04d.png

sudo apt-get install htop

htop

# second terminal ... wait, run, one at a time or upgrade VirtualBox from 8GB RAM allocation
cd /home/mshaffer/Desktop/sandbox-1828/
convert -verbose -density 600 -quality 100 ./americandictiona02websrich.pdf ./quality-100/V2-%04d.png

# decompose pdf to smaller paged pdfs command line linux
# pdftk
# qpdf is opensource 
# https://askubuntu.com/questions/221962/how-can-i-extract-a-page-range-a-part-of-a-pdf/672001#672001
## gs directly 
## Save this as a shell script, like pdfextractor.sh:
## gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dFirstPage=1 -dLastPage=10 -sOutputFile=output.pdf input.pdf
## If you have a huge document and need to split all pages, it is really fast and useful. 
## pdfseparate sample.pdf sample-%d.pdf
## change workflow... qpdf into single pages first step... will reduce this bottleneck of RAM explosion!
## qpdf --split-pages big.pdf part_%d.pdf


# sandbox-1828/data/V1-0001/page.pdf
#                           page.png (quality 100)
#							deskew.txt (angle)
#							rotate.png (page + angle)
#							white.png (rotate + white greyscale, fred's script)
#							white.hocr (page-level HOCR with columns)


# from above, I can then do some algorithm to identify words, page, column, with remainders spilling over ...





## fred's scripts into fred 
## http://www.fmwconcepts.com/imagemagick/textcleaner/index.php
## textcleaner runs deskew within
## imagemagick deskew calculate angle
# convert input.jpg -deskew 40 -format "%[deskew:angle]" info:
# -write info:info_paged.txt

# bash to doo for loop over the DIR.  use PHP cli

convert V1-0010.png -deskew 40 -format "%[deskew:angle]" info:
convert V1-0010.png -deskew 40 -format "%[deskew:angle]" info: > V1-0010-deskew.txt












































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



