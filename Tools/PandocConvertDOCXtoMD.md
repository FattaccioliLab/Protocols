Convert MS Word DOCX Files to Markdown with Images

Jul 8th, 2019

I don’t know when was the last time I received a Microsoft Word .docx file. However long the streak may have been: it has been broken today.

The document contained links and embedded images. I was instantly taken aback by the prospect of all the manual labor of extracting the images and saving them to files, not even knowing how MS Word behaves nowadays.

But I have pandoc installed.

And it’s great. It even extracts images and saves them into a subfolder. I love it. Didn’t know about this feature until I scrolled through the output of pandoc -h.

This is the command I used:

$ pandoc -o output.md --extract-media=./ inputfile.docx

Source : https://christiantietze.de/posts/2019/07/convert-docx-to-markdown/
