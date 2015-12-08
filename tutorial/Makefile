
TARGET=$(wildcard ./*.tex)

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

paper: $(TARGET) svg $(DOT:.dot=.pdf)

	TEXFONTS=:./fonts TEXINPUTS=:./fonts:./sty lualatex --shell-escape $<

clean:
	rm -f *.aux *.log *.snm *.out *.toc *.nav *intermediate *~ *.glo *.ist $(SVG:.svg=.pdf) $(DOT:.dot=.svg) $(DOT:.dot=.pdf)

cleanpdfs:
	rm -f $(TARGET)

cleanbbls:
	rm -f $(TARGET:.pdf=.bbl)


distclean: clean cleanpdfs cleanbbls
