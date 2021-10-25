# Protocol for photomask file drawing and conversion

At IPGG, there are two ways to create photomasks : 

- A film photoplotter, very good for masks with features larger than 10-20 µm,

- A chrome-quartz masker (Heidelberg) with minimal feature of 1 µm

## 1. Type of maskers at the IPGG technological  platform

### Photoplotter

The mask printer might only recognize the **.gbr** file, we have to
transfer our photomask design file into it before sent it to engineer.

### Heidelberg µPG 101

The masker is able to work with different file formarts : gds II or dxf

## 2. Design procedure

### 2.1 Why going from CleWin to Autocad + KLayout ?

Several reaons for that :

- XOR mode on Clewin is very inefficient. The µPG 101 has an embedded XOR mode that is way better

- DXF are natively recognized by laser masking systems

- CleWin is expensive, even for academia, whereas Autocad is proprietary but free, and KLayout open-source and free

### What it an XOR mode ?

<img src="file:///Users/jacques/Github/Protocols/Microfabrication/Photomask%20Design%20and%20Conversion/media/XORMode.png" title="" alt="XORMode.png" width="497">

Source : Heidelberg µPG 101 Manual [[here](./media/upg101_manual.pdf)]

The µPG 101 is able to automatically do the XOR combination of drawings if proper rules are used, when you'll work with DXF.

This option does not apply for other formats (GDS, CIF, BMP).

### Strategy

- Draw the design by **AutoCAD** and save it as **.dxf** file 

- Then use **Klayout**  to check it 

- If you use the phoplotter, convert it to  **.gds** file



**Attention:** Don't use AutoCAD save as **.gds** file directly, it will
lead to some recognition error of mask printer. And it\'s better not to
use **CleWin5** directly to design your mask, because some operation
will leave many extra lines which will be a disaster for some mask print
way.



**Autocad** is free of charge with an academic licence.

**Klayout** could be downloaded freely free of charge
<https://www.klayout.de/build.html>. 

A license is needed by **CleWin5**, we'd better ask the engineer for help about some operation.



## 3. Detailed procedure.

### 3.1 Draw your mask layout with Autocad

#### 3.1.1 Set the unit as microns in the AutoCAD.

Click **Format**→**Units** and select **Microns**.

![](.//media/image1.png)

![](.//media/image2.png)

#### 3.1.2 Read the following rules to make a DXF compatible with the masker !

Heidelberg provides a very good cheat sheet with the rules to follow to make a compatible dxf :

1. Use a 100% Autocad compatible editor. Try to load the file to Autocad itself and make sure, the file can be loaded. Namely : **AutoCAD** and **KLayout**.

2. Always join polylines correctly, be especially cautious, when using arcs within a polyline : **PEDIT**

3. Only one font is provided with the dxf conversion package. The dxf standard font will replace any font selected in the DXF-design.

4. Only the following attributes assigned to a text are supported: ROTATION, MIRRORING, SCALING.

5. Avoid placing structures in layer 0.

6. Do not use special characters in the layer names.

7. Try to design by means of the metric system. 

8. Polylines with widths must not have a change in its widths (tapered lines).

9. Various scaling in x and y when inserting a block is not supported.

10. External blocks are not supported.

11. Try to use only the following entities: CIRCLE, POLYLINE / LWPOLYLINE (with or without width), and TEXT.

12. Although our dxf translator supports newer dxf releases, we recommend to use **DXF Release 12**.

13. Avoiding the XOR mode on AutoCAD using the XOR mode with the µPG 101

#### 3.1.3 Draw your mask design in AutoCAD,

Every pattern and line must be a closed polygon closed in order to be recognized by printer. 

**3.** The diameter of common wafer
is 4 inches (\~10.16 cm). It's better to use the pattern like

![](.//media/image3.png)

to mark the boundary of the wafer and each chip
which make the further cutting easier as shown below.

![](.//media/image4.png)

**4.** Save your design as **.dxf** file.

Click **File**→**Save As** and select **AutoCAD DXF Release 12 (\*.dxf)**.

![](.//media/image6.png){width="2.3108136482939634in" height="4.175in"}
<img src=".//media/image7.png" title="" alt="" width="422">



#### 3.1.3 Check your mask design in KLayout

Open Klayout (Editor), click **File→Reader Option** and select
\"**Merge lines and auto-close open contours**\" option under the label
DXF, then import the **.dxf** file.

<img title="" src=".//media/image9.png" alt="" width="490">

Check your pattern and ensure every line and area is normal. 



1. If you use the Photoplotter, please go to **File**→**Save As** and select **GDS2 files**.

2. If you use the µPG, you can save it as a **DXF**. Caution : use a PC with Windows (Linux : not tested !) as a DXF on MacOS will give some errors on the machine.

![](.//media/image10.png)


If there are more than one layer in your file, please integrate them
into one layer or make sure other unrelated layers (such as label or
mark layer, etc.) are inactive and select **Layers to save visible
layers only** option as shown below.



![](.//media/image12.png)

Then you can send this **.GDS** file to engineer and ask them to help
you complete the final format conversion to **.gbr** file (as shown in
**Step 6**).

### 3.5 Use **CleWin5** to convert the **.GDS** file to a **GBR** file.

This last step is only for the photoplotter and is not *necessary*. Basically, the dxf or the gds are sufficient to be sent to the engineers.

You need to give the polarity of the mask, to be sure to have it printed the good way.

There is a 5 inch mask mark in the background, select your pattern and
move it to overlap the mark.

![](.//media/image13.png)
![](.//media/image14.png)

Click **File**→**Export layer** and select **Gerber RS-274X files
(\*.gbr)** option.

![](.//media/image15.png){width="3.335505249343832in"
height="3.048987314085739in"} ![](.//media/image16.png){width="2.85in"
height="3.7711034558180225in"}

This **.gbr** file could be sent to engineer for printing your
photomask.
