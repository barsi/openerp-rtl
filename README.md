OpenERP Arabic Report Support:
==============================

This is an Openerp patch to fix issues occured when dealing with Arabic and other RTL languages (Arabic, Hebrew, Ordo, Farsi, etc). 


## <u>Installation on Windows</u>: 
   
 1.  copy file **arabic_reshaper.py** into:
        `<INSTALL_DIR>\Openerp Server 6.1\Server\server`,  where `<INSTALL_DIR>` is the location where you installed Openerp Server (e.g. C:\Program Files).
2. copy folder **bidi** into the same Location you put **arabic_reshaper.py** to it:
        `<INSTALL_DIR>\Openerp Server 6.1\Server\server`
3. copy file **textobject.py** into:
        `<INSTALL_DIR>\Openerp Server 6.1\Server\server\reportlab\pdfgen`, you may want to backup the old **textobject.py** before replace it with this version.

### Creating Custom Fonts Hosting Directory:
1. create a new directory name "fonts" inside:
        	`<INSTALL_DIR>\Openerp Server 6.1\Server\server\`

2. open a file called **openerp-server.conf** with your preferred text editor
        	(e.g. notepad), the **openerp-server.conf** live in:
        	`<INSTALL_DIR>\Openerp Server 6.1\Server\server\openerp-server.conf`

3. at the end of the file, add the following line:<br>
        	`fonts_search_path = <INSTALL_DIR>\Openerp Server 6.1\Server\server\fonts`
        	<blockquote>
        	**NOTE:** Dont forget to replace <INSTALL_DIR> with the absolute path of OpenERP server installation (e.g. C:\Program Files).
		</blockquote>
4. go to DjaVu Fonts Site http://dejavu-fonts.org/wiki/Download and download a file called **dejavu-fonts-ttf-2.33.tar.bz2**,  [here](http://ie.archive.ubuntu.com/ftp.frugalware.org/pub/frugalware/frugalware-current/source/x11/dejavu-ttf/dejavu-fonts-ttf-2.33.tar.bz2) is another mirror for it.

5. extract **dejavu-fonts-ttf-2.33.tar.bz2** and copy the contents of "ttf" folder into your fonts directory:
        	`<INSTALL_DIR>\Openerp Server 6.1\Server\server\fonts`

6. Now, restart openerp server:

        	-  Control Panel => Administrative Tools => Services
        	-  find a service called openerp server
        	-  restart it.
        	
7. try to print some reports that contains arabic characters. enjoy :)

> more information can be found on our blog: 
> [http://goure-it.blogspot.com](http://goure-it.blogspot.com).


##  Installation on Linux:

<blockquote>    	Because There are several ways to install OpenERP on Linux, Files Locations
    are not unique. so, this instructions assume that you install OpenERP using
     the popular method, Through `apt-get` on ubuntu platform.</blockqoute>

1. Copy the file "textobject.py" into:
			`/usr/lib/python2.6/dist-packages/reportlab/pdfgen/textobject.py`
		make sure you backup old `"textobject.py"` before you replace it.

2. Check to ensure if the link file:
			`/usr/share/pyshared/reportlab/pdfgen/textobject.py`
		pointing correctly to the new `"textobject.py"` file.

3. Copy `"arabic_reshaper.py"` file, and `"bidi"` directory into:
			`/usr/lib/python2.6/dist-packages/`

4. Create a folder called `"fonts"` in a location that is accessable by openerp server. (e.g. ` /usr/share/pyshared/fonts`).

5.  go to [DejaVu Fonts Site]( http://dejavu-fonts.org/wiki/Download) and download a file called **dejavu-fonts-ttf-2.33.tar.bz2** [here] [id] is another mirror for it:
[id]: http://ie.archive.ubuntu.com/ftp.frugalware.org/pub/frugalware/frugalware-current/source/x11/dejavu-ttf/dejavu-fonts-ttf-2.33.tar.bz2 "Ubuntu Mirror"

6. extract **dejavu-fonts-ttf-2.33.tar.bz2** copy the contents of a folder called **ttf** and paste them into "fonts" directory you created on step **4**.

7. use linux searching tool, search for a file called **openerp-server.conf**, open it with a text editor (e.g. gedit), at the end of it, paste the following line:

       **fonts_search_path = /usr/share/pyshared/fonts**
 where `/usr/share/pyshared/fonts` is your new fonts directory you created on step **4**.

8. restart openerp server, `sudo service openerp restart` go and try printing some reports with arabic characters.


## Using Fancy Fonts for your reports:
as you might noticed, using dejavu fonts are so uguly on arabic characters.
there is a set of awesome arabic fonts (open source) created by arabeyes:
[Khotot](http://projects.arabeyes.org/project.php?proj=Khotot)
go and download them.

### Changing Report Fonts Strategy:
   Keep in mind that openerp report engine depends on 4 standard PDF fonts:
  
  1. Helvetica
  2. Times
  3. Times-Roman
  4. Courier

all 4 fonts unable to render most languages correctly. as a result, openerp report enginge will automagically pickup DjaVu Fonts Set, when you point to them.

That's why you set `fonts_search_path = /your/custom/fonts`  option in openerp-server.conf file before. here is the mapping that openerp report engine does:

<table>
<thead>
		<tr><th> Font Name</th> <th>Font Type</th>       <th>DjaVu Equivelant</th></tr>
</thead>
<tbody>
<tr>
		<td> Helvetica  </td><td>        normal		</td><td>	   DejaVuSans.ttf</td>
</tr>
<tr>
		<td> Helvetica    </td><td>      bold	</td><td>		   DejaVuSans-Bold.ttf</td>
</tr>
<tr>
		<td> Helvetica      </td><td>    italic		</td><td>	   DejaVuSans-Oblique.ttf</td>
</tr>
<tr>
		<td> Helvetica  </td><td>      bolditalic	</td><td>	   DejaVuSans-BoldOblique.ttf</td>
		 
</tr>
<tr><td>----</td><td>----</td><td>----</td></tr>
<tr>
		<td> Times </td><td>         normal	</td><td>		   LiberationSerif-Regular.ttf</td>
</tr>
<tr>
		<td> Times      </td><td>    bold			</td><td>   LiberationSerif-Bold.ttf</td>
</tr>
<tr>
		<td> Times   </td><td>       italic		</td><td>	   LiberationSerif-Italic.ttf</td>
		 
</tr>
<tr>
		<td> Times  </td><td>        bolditalic	</td><td>	   LiberationSerif-BoldItalic.ttf</td>
		 
</tr>
<tr><td>----</td><td>----</td><td>----</td></tr>
<tr>
		<td> Times-Roman</td><td>    normal		</td><td>	   LiberationSerif-Regular.ttf</td>
</tr>
<tr>
		 <td>Times-Roman  </td><td>  bold		</td><td>	   LiberationSerif-Bold.ttf</td>
</tr>
<tr>
		<td> Times-Roman  </td><td>  italic	</td><td>		   LiberationSerif-Italic.ttf</td>
</tr>
<tr>
		 <td>Times-Roman </td><td>   bolditalic	</td><td>	   LiberationSerif-BoldItalic.ttf</td>
</tr>
<tr><td>----</td><td>----</td><td>----</td></tr>
<tr>
		<td> Courier     </td><td>   normal	</td><td>			FreeMono.ttf</td>
</tr>
<tr>
		 <td>Courier </td><td>       bold		</td><td>		FreeMonoBold.ttf</td>
</tr>
<tr>
		<td>Courier     </td><td>   italic		</td><td>		FreeMonoOblique.ttf</td>
</tr>
<tr>
		<td> Courier  </td><td>      bolditalic		</td><td>	FreeMonoBoldOblique.ttf</td>
</tr>
<tr><td>----</td><td>----</td><td>----</td></tr>
</tbody>

</table>

 So, for example. if you want to replace `Helvetica` with something else, (e.g. `ae_AlMohanad.ttf` from arab eyes package), you can do it by renaming your font 
**DejaVuSans.ttf** and put it into your custom fonts directory.

For More Information, go to our [blog](http://goure-it.blogspot.com)

Copyrights &copy; Mohammed Barsi (dantario AT gmail DOT com).

Credits:
========
Many Thanks go to Meir Kriheli and Abd Allah Diab for their unicode bidirection packages:

- python-bidi package created by  Meir Kriheli http://github.com/mksoft/python-bidi 
	"GNU Library or Lesser General Public License (LGPL)"
- arabic_reshaper.py created by Abd Allah Diab https://github.com/mpcabd/python-arabic-reshaper 
	"GNU General Public License v3."