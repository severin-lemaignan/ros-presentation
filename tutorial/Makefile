
TARGETLIST=$(wildcard ./*.tex)
TARGET=$(TARGETLIST:.tex=.pdf)

DOT=$(wildcard figs/*.dot)
SVG=$(wildcard figs/*.svg)

all: paper

$(SVG:.svg=.pdf): %.pdf: %.svg
	inkscape --export-pdf $(@) $(<)

%.aux: paper

svg: $(SVG:.svg=.pdf)

%.svg: %.dot

	twopi -Tsvg -o$(@) $(<)

%.bbl: %.aux
	biber $(<:.aux=)

bib: cleanbbls $(TARGET:.pdf=.bbl)


%.pdf: %.tex
	TEXFONTS=:./fonts TEXINPUTS=:./fonts:./sty lualatex --shell-escape $<

paper: svg $(TARGET) $(DOT:.dot=.pdf)

clean:
	rm -f *.aux *.log *.snm *.out *.toc *.nav *intermediate *~ *.glo *.ist $(SVG:.svg=.pdf) $(DOT:.dot=.svg) $(DOT:.dot=.pdf)

cleanpdfs:
	rm -f $(TARGET)

cleanbbls:
	rm -f $(TARGET:.pdf=.bbl)


distclean: clean cleanpdfs cleanbbls
