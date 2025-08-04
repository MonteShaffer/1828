# install imagemagick with ghostscript

sudo apt update && sudo apt upgrade
sudo apt install libpng-dev libjpeg-dev libtiff-dev

sudo apt-get install ghostscript
sudo apt-get install imagemagick

sudo apt install tesseract-ocr   
tesseract --version   

# setup policy
## <policy domain="coder" rights="read|write" pattern="PDF" />
## resource memory|disk to 4GiB

sudo nano /etc/ImageMagick-6/policy.xml

convert --version
# 6.9? we are in convert space, not magick space???

# split large PDFs into smaller ones 
sudo apt-get install qpdf 

qpdf --split-pages americandictiona01websrich.pdf V1-page.pdf
qpdf --split-pages americandictiona02websrich.pdf V2-page.pdf

# https://archive.org/stream/americandictiona01websrich#page/4/mode/2up
# https://archive.org/stream/americandictiona02websrich#page/4/mode/2up
# ORIGINAL FILES > 100 MB, so moved outside of REPO.

# write PHP script to move single-page PDFs and render the necessary loops 

## page.png 

/home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V1-page-0022.pdf


cd /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/
mkdir ./V1-0022/
cp V1-page-0022.pdf ./V1-0022/page.pdf

convert -verbose -density 600 -quality 100 ./V1-0022/page.pdf ./V1-0022/page.png

convert ./V1-0022/page.png -deskew 40 -format "%[deskew:angle]" info: > ./V1-0022/deskew.txt

#convert ./V1-0022/page.png -rotate 0.321726 ./V1-0022/rotate.png
convert ./V1-0022/page.png -distort SRT 0.321726 ./V1-0022/rotate.png

sh /home/mshaffer/Documents/GitHub/1828/sandbox-1828/fred/textcleaner -g -e stretch -f 15 -o 5 ./V1-0022/rotate.png ./V1-0022/white.png

tesseract -c tessedit_debug_fonts=1 --psm 1 ./V1-0022/white.png ./V1-0022/white -l eng hocr 


# sudo apt install php-cli
# need cli 


##
#Additionally, some users have noted that while tessedit_debug_fonts can be used to debug font recognition, it often outputs too much information at the character level, which is sent to stdout rather than the HOCR file.
#This can make it difficult to extract meaningful font-related data from the output.

#In some cases, the issue may be related to the version of Tesseract being used. For example, in Tesseract 4 and later versions, the ability to retrieve font information in HOCR format has been limited or changed, and users have reported that hocr_font_info 1 does not return the font name as expected.

#Furthermore, it is important to note that font attribute recognition, including italic and bold, is primarily supported in the legacy engine (e.g., --oem 0), and not in the newer LSTM engine used in Tesseract 4 and later.
#This means that if you are using the LSTM engine, you may not get accurate or reliable font attribute information, even with tessedit_debug_fonts enabled.

#If you are experiencing issues with tessedit_debug_fonts not showing up in HOCR, it may be necessary to use the legacy engine or consider alternative approaches, such as training Tesseract on specific fonts to improve recognition accuracy.

java -jar /home/mshaffer/Desktop/hocrViewer/JPageViewer.jar ./V1-0022/white.hocr ./V1-0022/white.png

# sandbox-1828/data/V1-0001/page.pdf
#                           page.png (quality 100)
#							deskew.txt (angle)
#							rotate.png (page + angle)
#							white.png (rotate + white greyscale, fred's script)
#							white.hocr (page-level HOCR with columns)


# from above, I can then do some algorithm to identify words, page, column, with remainders spilling over ...
	# maybe do hocr again at the word-level with legacy tools to identify bold/italic ... 
	# it would be nice to "find the font" for the dictionary ... train with the specific font...
	
cd /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/	
# 0.54
convert ./V2-290/page.png -deskew 20 -format "%[deskew:angle]" info:
convert ./V2-290/page.png -deskew 40 -format "%[deskew:angle]" info:
convert ./V2-290/page.png -deskew 80 -format "%[deskew:angle]" info:

# 5.34
convert ./V2-290/white.png -deskew 20 -format "%[deskew:angle]" info:
convert ./V2-290/white.png -deskew 40 -format "%[deskew:angle]" info:
convert ./V2-290/white.png -deskew 80 -format "%[deskew:angle]" info:



V2-889
convert ./V2-889/page.png -deskew 20 -format "%[deskew:angle]" info:
convert ./V2-889/page.png -deskew 40 -format "%[deskew:angle]" info:
convert ./V2-889/page.png -deskew 80 -format "%[deskew:angle]" info:

convert ./V2-889/white.png -deskew 20 -format "%[deskew:angle]" info:
convert ./V2-889/white.png -deskew 40 -format "%[deskew:angle]" info:
convert ./V2-889/white.png -deskew 80 -format "%[deskew:angle]" info:


convert ./V2-549/rotate.png -distort SRT -1 ./V2-549/monte.png
convert ./V2-549/rotate.png -distort SRT 1.1090257167816162 ./V2-549/monte2.png


convert ./V2-549/page.png -distort SRT -0.269744873046875 ./V2-549/monte2.png
convert ./V2-549/page.png -distort SRT 0.269744873046875 ./V2-549/monte3.png
convert ./V2-549/page.png -distort SRT 5 ./V2-549/p5.png
convert ./V2-549/p5.png -distort SRT -4.759155750274658 ./V2-549/p5reverse.png
convert ./V2-549/page.png -distort SRT -0.017944183200597763 ./V2-549/rotate.png

convert -verbose -density 600 -quality 100 ./V2-549/page.pdf ./V2-549/page.png
python3 /home/mshaffer/Documents/GitHub/1828/-code-/run/php/projects/1828/skew-ai.py -i /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V2-549/page.png

0.269744873046875
convert ./V2-549/page.png -distort SRT 0.269744873046875 ./V2-549/rotate.png

###

python3 /home/mshaffer/Documents/GitHub/1828/-code-/run/php/projects/1828/skew-ai.py -i /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V1-0827/page.png

# if zero, just do a copy
convert ./V1-0827/page.png -distort SRT 0.0 ./V1-0827/rotate.png


###
convert -verbose -density 600 -quality 100 ./V2-225/page.pdf ./V2-225/page.png

python3 /home/mshaffer/Documents/GitHub/1828/-code-/run/php/projects/1828/skew-ai.py -i /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V2-225/page.png

# if zero, just do a copy
convert ./V2-225/page.png -distort SRT 0.21346282958984375 ./V2-225/rotate.png


###
convert -verbose -density 600 -quality 100 ./V2-063/page.pdf ./V2-063/page.png

python3 /home/mshaffer/Documents/GitHub/1828/-code-/run/php/projects/1828/skew-ai.py -i /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V2-063/page.png

# if zero, just do a copy
convert ./V2-063/page.png -distort SRT 0.8970413208007812 ./V2-063/rotate.png


###
convert -verbose -density 600 -quality 100 ./V2-644/page.pdf ./V2-644/page.png

python3 /home/mshaffer/Documents/GitHub/1828/-code-/run/php/projects/1828/skew-ai.py -i /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V2-644/page.png

# if zero, just do a copy
convert ./V2-644/page.png -distort SRT 1.1070327758789062 ./V2-644/rotate.png

V2-644











convert ./V2-714/page.png -distort SRT 0.36540183424949646 ./V2-714/monte.png




tesseract --psm 1 ./V1-0545/white.png ./V1-0545/monte -l eng hocr 

# y
convert ./V1-0545/rotate.png -threshold 50% -negate -crop x1 -format "%[fx:w*h*mean]\n" info:
# x
convert ./V1-0545/rotate.png -threshold 50% -negate -crop 1x -format "%[fx:w*h*mean]\n" info:
# plot 
convert ./V1-0545/rotate.png -threshold 50% -negate -crop 1x -format "%[fx:w*h*mean]\n" info: | gnuplot -e 'plot "-" using 1: xtic(1) with histogram' -persist
# BINGO ... 3 columns 
# find min values about 1/3 of the way and 2/3 of the way ... crop columns 


convert ./V1-0545/rotate.png -threshold 50% -negate -crop 1x -format "%[fx:w*h*mean]\n" info: > ./V1-0545/horizontal.txt

# BINGO, use 10 as minimum, reach 10, stays there ... wait until gets greater than 10 ... left/right of gutter 
# 30-160 will be vertical column lines ... 
# nonparametric smoothing? not loess, but kde = kernal density estimates 
# search in 0.2-0.4 region 0.5-0.8 region for two minimum 

889-908 is gutter 1 (about 20 pixels wide for V1, would be double that for V2)
1724-1771 is gutter 2

889 is first "1" or "0", so crop one pixel later 
0-890
908-1725 ... 1727
1771-end 

GIMP width = 890, offset = 0
GIMP width = 819, offset = -908

3rd one from the right 
end = 2712
1771 - 2712 = 941
2712 - 890-819 = 1003, offset = 908 + 819 + 12? = 1739

GIMP width = 941, offset = -1739


# using R run script with libraries from command line
# crop into columns after we find two minimum

page.png
rotate.png
c1, c2, c3.png 
white-c1, white-c2, white-c3.png
c1.hocr, c2.hocr, c3.hocr

tightly crop c1,c2,and c3 (begin/end analysis as well)
store json object with crop parameters, so if we do a page-level HOCR overlay we have some offsets for each column (back to rotate.png)

2564 is right column end 
72 is left column begin (noise at beginning)

each column is about 820 pixels wide ...


# sudo apt install r-base r-base-dev -y
 # my_script.R
    library(ggplot2) # Load the ggplot2 library
    # Your R code that uses ggplot2 functions
    data <- data.frame(x = 1:10, y = rnorm(10))
    print(ggplot(data, aes(x, y)) + geom_point())
    
    Rscript my_script.R
    
Rscript --vanilla ...
write Rscript template, use PHP to do replaces?       







# Additionally, if you need to ensure that the image's virtual canvas is properly handled, you can use the +repage option before and after the crop operation:
convert input.jpg +repage -crop WxH+X+Y +repage output.jpg

# X,Y = top-left
# W, H = widtth--height 

# create a font for 1828 Noah Webster
# https://www.calligraphr.com/en/pricing/
# https://fontforge.org/en-US/

# /home/mshaffer/Documents/GitHub/1828/sandbox-1828/data/V1-0545/ ... has numbers 



### https://stackoverflow.com/questions/28591117/how-do-i-segment-a-document-using-tesseract-then-output-the-resulting-bounding-b
## hocrViewer... maybe an frame similar to what I did with mturk on patent documents, review the java implementation ...
## load IMAGE, load HOCR, build result ... 
# https://www.primaresearch.org/tools/PAGEViewer
# sudo apt install default-jdk

# sudo apt install python3 python3-pip

# https://docs.scribeocr.com/tesseract_users.html

# https://github.com/tesseract-ocr/tesseract/issues/2781
# italics is now font-detection with new classifier?
# tesseract 3 does bold/italics identification... newer version does not!

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



