---
title: Computer Vision
image: img/timeline/cv.jpg
notes: show image of opencv determining gauge value
---
*Computer Vision enabled a key component of Gauge Reader: the ability to flexibly translate an analog gauge reading to a digital value.*\\
\\
Computer Vision allows a computer to understand information about the physical world -- or in my case, allows a computer to read [various](#modal4){:data-toggle="modal"} [types](#modal5){:data-toggle="modal"} [of](#modal6){:data-toggle="modal"} [analog](#modal7){:data-toggle="modal"} [gauges](#modal8){:data-toggle="modal"}.\\
\\
Just like electronic hardware design and production, Computer Vision was an area about which I knew very little.  After reviewing multiple academic papers<sup>[1](http://www.hindawi.com/journals/mpe/2015/283629/), [2](http://www.imeko.org/publications/tc4-2008/IMEKO-TC4-2008-122.pdf), [3](http://www.asee.org/documents/zones/zone1/2014/Student/PDFs/116.pdf), [4](http://www.jcomputers.us/vol9/jcp0904-01.pdf)</sup> on using Computer Vision with analog gauges, I began using Python and [OpenCV](http://opencv.org) to design an algorithm that could quickly and accurately read the image of an analog gauge.\\
\\
Within three weeks I had an algorithm that could read many analog gauges in addition to a web-based tuning <abbr class="initialism" title="User Interface">UI</abbr> so that the system could quickly be adapted to new gauge faces. Pretty awesome to see the messy physical world translated to the binary world.
