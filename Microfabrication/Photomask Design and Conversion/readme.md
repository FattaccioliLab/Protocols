# Protocol for photomask file drawing and conversion



At IPGG, there are two ways to create photomasks : 

- A film photoplotter, very good for masks with features larger than 10-20 µm,

- A chrome-quartz masker (Heidelberg) with minimal feature of 1 µm



## Photoplotter

The mask printer might only recognize the **.gbr** file, we have to
transfer our photomask design file into it before sent it to engineer.

## Heidelberg µPG 101

The masker is able to work with different file formarts : gds II or dxf



## Design procedure

The strategy is:



- Draw the design by **AutoCAD** and save it as **.dxf** file 

- Then use **Klayout**  to check it 

- If you use the phoplotter, convert it to  **.gds** file



**Attention:** Don't use AutoCAD save as **.gds** file directly, it will
lead to some recognition error of mask printer. And it\'s better not to
use **CleWin5** directly to design your mask, because some operation
will leave many extra lines which will be a disaster for some mask print
way.



**Klayout** could be downloaded freely free of charge
<https://www.klayout.de/build.html>. 

A license is needed by **CleWin5**, we'd better ask the engineer for help about some operation.



Here the detailed procedure.

**1.** Set the unit as Micro in the AutoCAD.

Click **Format**→**Units** and select **Microns**.

![](.//media/image1.png){width="2.7708333333333335in"
height="3.1063156167979002in"}
![](.//media/image2.png)

{width="2.0962390638670167in"
height="3.1145833333333335in"}



**2.** Draw your mask design in AutoCAD, every pattern and line must be
closed in order to be recognize by printer. Heidelberg provides a very good cheat sheet with the rules to follow to make a compatible dxf : 





<img title="" src=".//media/dxf_Rules.png" alt="" data-align="inline">



**3.** The diameter of common wafer
is 4 inches (\~10.16 cm). It's better to use the pattern like


![](.//media/image3.png)

{width="0.4867793088363955in"
height="0.46875in"} 

to mark the boundary of the wafer and each chip
which make the further cutting easier as shown below.

![](.//media/image4.png){width="4.054390857392826in" height="4.0625in"}

**3.** Confirm the polarity (positive or negative) of photomask
according to the pattern and photoresist you used. You have to fill the
area solid where you want to mask as the following example shown, this
example was used for negative photoresist.

![](.//media/image5.png){width="3.975in" height="3.9269149168853894in"}

**4.** Save your design as **.dxf** file.

Click **File**→**Save As** and select **AutoCAD 2018 DXF (\*.dxf)**.

![](.//media/image6.png){width="2.3108136482939634in" height="4.175in"}
![](.//media/image7.png){width="3.783333333333333in"
height="4.180261373578302in"}

**5.** Open Klayout (Editor), click **File→Reader Option** and select
\"**Merge lines and auto-close open contours**\" option under the label
DXF, then import the **.dxf** file.

![](.//media/image8.png){width="3.1916841644794403in"
height="3.345812554680665in"}
![](.//media/image9.png){width="3.1921456692913384in" height="3.35in"}

Check your pattern and ensure every line and area is normal. Click
**File**→**Save As** and select **GDS2 files**.

![](.//media/image10.png){width="2.797351268591426in"
height="2.933333333333333in"}
![](.//media/image11.png){width="3.4960509623797025in"
height="2.8368055555555554in"}

If there are more than one layer in your file, please integrate them
into one layer or make sure other unrelated layers (such as label or
mark layer, etc.) are inactive and select **Layers to save visible
layers only** option as shown below.

![](.//media/image12.png){width="6.5in" height="5.063194444444444in"}

Then you can send this **.GDS** file to engineer and ask them to help
you complete the final format conversion to **.gbr** file (as shown in
**Step 6**).

**6.** Open **CleWin5** and import the **.GDS** file.

There is a 5 inch mask mark in the background, select your pattern and
move it to overlap the mark.

![](.//media/image13.png){width="3.440926290463692in"
height="2.556800087489064in"}
![](.//media/image14.png){width="2.8081780402449694in"
height="2.582563429571304in"}

Click **File**→**Export layer** and select **Gerber RS-274X files
(\*.gbr)** option.

![](.//media/image15.png){width="3.335505249343832in"
height="3.048987314085739in"} ![](.//media/image16.png){width="2.85in"
height="3.7711034558180225in"}

This **.gbr** file could be sent to engineer for printing your
photomask.
