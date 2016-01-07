#IUST HTMLCharDet

IUST HTMLCharDet is a java tool for detecting *charset encoding* of HTML web pages. **HTMLCharDet** stands for _**HTML** **Char**set **Dete**ctor_ and **IUST** stands for _**I**ran **U**niversity of **S**cience & **T**echnology_.

This tool is in connection with a paper entitled:  
<p align=center style="font-size:160%;">
 <b>Charset Encoding Detection of HTML Documents</b></br>
 <em><b>A Practical Experience</b></em></br>
</p>

which was presented in the *[11th Asia Information Retrieval Societies Conference][1]*, in *Brisbane*, *Australia*, *2015*.

Although we wrote a paper to describe the algorithm, but this tool is not just an academic effort to solve *charset encoding detection* problem for HTML web pages. In fact this tool is an **industrial** product which is actively used in a large-scale web crawler,  continuously under a load of over than **1 billion** web pages.

##Precision (quick view)

In order to determine the precision of IUST HTMLCharDet, we compared it with the two famous charset detector tools namely _**IBM ICU**_ and _**Mozilla CharDet**_ against two test scenario, i.e. **Encoding-Wise** and **Language-Wise**. Results of the comparisons are presented in the [*paper*][paper], but bellow you can have a glance at results. To read more about comparisons, please find the paper inside the *wiki* folder.

**Note:** In these images *Hybrid* is the same *IUST HTMLCharDet*, in the paper we called it *Hybrid* because it is actually a hybrid mechanism.

####Encoding-Wise
In this test scenario, we compared *IBM ICU*و *Mozilla CharDet* and the *hybrid mechanism* against a corpus of HTML documents. To create this corpus, we wrote a multi-threaded crawler and then we gathered a collection of nearly 2700 HTML pages with various charset encoding types. The code which we wrote for creating this corpus is available in the [*./src/test/java/encodingwise/corpus*][corpus-code] folder of this repository and the created corpus is available via [*./test-data/encoding-wise/corpus.zip*][corpus-data]. Bellow find the comparison results ...

<p align=center>
<img src="https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/wiki/README-images/encoding-wise-eval.jpg" alt="encoding-wise evaluation image" height="450" width="766">
</img>
</p>
Usually graphical presentation of the results makes a better sense ...

<p align=center>
<img src="https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/wiki/README-images/encoding-wise-eval-diagram.jpg" alt="encoding-wise evaluation diagram image" height="300" width="645">
</img>
</p>

####Language-Wise
In this test scenario, we compared our *hybrid mechanism* with the two others from language point of view. In this connection, we collected a list of URLs that are pointing to various web pages with different languages. The URLs are selected from the **top 1 million websites** visited from all over the world, as reported by [*Alexa*][Alexa]. In order to collect HTML documents in a specific language, we investigated web pages with the internet domain name of that language. For example, *Japanese* web pages are collected from *.jp* domain. The results of evaluation for eight different languages are shown in details in the following table ...

<p align=center>
<img src="https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/wiki/README-images/language-wise-eval.jpg" alt="language-wise evaluation image" height="305" width="765">
</img>
</p>
To find more details about this test, you may want to have a look at: [*./test-data/language-wise/results/*][lang-wise-results]. 

<p align=center>
<img src="https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/wiki/README-images/language-wise-eval-diagram.jpg" alt="language-wise evaluation diagram image" height="319" width="645">
</img>
</p>
##Installation
 
I'm about to deploy this tool to Maven Central, but before the first release you can build it as follows:

1. clone this repo into your local using `$ git clone https://github.com/shabanali-faghani/IUST-HTMLCharDet.git`
2. run `$ mvn clean install` on the cloned-repo's root directory
3. find the `jar` file in `target` folder or in the `~/.m2` directory
4. also you need the first 4 dependency that were mentioned in the [*pom.xml*][pom] file to get it to work for you.

##Usage

If you trust in the Web Server or trust in the Website that the pages are crawled from, you can use this tool as follows:
```java
String charset = HTMLCharsetDetector.detect(htmlByteArray, true);
```
otherwise, call detect method with `false` value for `lookInMeta` argument as follows:
```java
String charset = HTMLCharsetDetector.detect(htmlByteArray, false);
```
Also, there is another detection method with `#detect(byte[] rawHtmlByteSequence)` signature, but I don't recommend to use it. To see why, please refer to its [*javadoc*][javadoc].

[1]: http://airs-conference.org/2015/program.html
[paper]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/tree/master/wiki/Charset-Encoding-Detection-of-HTML-Documents.pdf
[corpus-code]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/tree/master/src/test/java/encodingwise/corpus
[corpus-data]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/tree/master/test-data/encoding-wise/corpus.zip
[Alexa]: www.alexa.com
[lang-wise-results]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/tree/master/test-data/language-wise/results
[pom]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/pom.xml
[javadoc]: https://github.com/shabanali-faghani/IUST-HTMLCharDet/blob/master/src/main/java/ir/ac/iust/selab/htmlchardet/HTMLCharsetDetector.java#L145
