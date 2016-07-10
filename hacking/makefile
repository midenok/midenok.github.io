# PREFIX = c:/cygwin64
DSLFILE = $(PREFIX)/usr/share/sgml/docbook/stylesheet/dsssl/modular/print/docbook.dsl
XMLDCL = $(PREFIX)/usr/share/sgml/declaration/xml1n.dcl
XSLTHL_JAR = $(PREFIX)/usr/local/lib/xslthl/xslthl.jar
XSLTHL_CONFIG = $(PREFIX)/usr/share/sgml/docbook/xsl-stylesheets/highlighting/xslthl-config.xml
SAXON = java -cp "$(PREFIX)/usr/local/lib/saxon/saxon.jar;$(XSLTHL_JAR)" -Dxslthl.config="file:///$(XSLTHL_CONFIG)" com.icl.saxon.StyleSheet

%.html: templ/docbook.html.xsl %.xml
	xsltproc -o $@ $^

%.fo: %.xml templ/docbook.fo.xsl
	$(SAXON) -o $@ $^

%.latex: templ/docbook.latex.xsl %.xml
	xsltproc -o $@ $^

%.tex: %.xml
	jade -b iso-8859-5 -d templ/docbook.dsssl -t tex -o $@ $(XMLDCL) $<

%.pdf: %.latex
	pdflatex -output-format pdf $<
	rm $(addprefix $(basename $@),.aux .glo .idx .log .out)

%-tex.pdf: %.tex
	pdfjadetex -output-format pdf $<

%-fop.pdf: %.fo
	fop -fo $< -pdf $@

all: hacking-cv.html

.PHONY: all
