TARGET   = paper
TEXFILES = $(wildcard *.tex)
FIGURES  = #ting-fig16 \


.SUFFIXES:	.plot .eps .fig

all: $(TARGET).pdf

figures/%.eps: plots/%.plot
	gnuplot $< > $@

graphs: $(addprefix figures/, $(addsuffix .eps, $(FIGURES)))

$(TARGET).aux: $(TEXFILES) 
	pdflatex $(TARGET).tex

$(TARGET).bbl: $(TARGET).aux
	bibtex $(TARGET)

$(TARGET).pdf: $(TARGET).bbl graphs
	pdflatex $(TARGET).tex
	pdflatex $(TARGET).tex

nobib:: $(addsuffix .eps, $(FIGURES)) $(TARGET).aux
	dvips $(TARGET).dvi -Ppdf -Pcmz -Pamz -t letter -D 600 -G0 -o $(TARGET).ps
	ps2pdf ${PS2PDF_FLAGS} $(TARGET).ps

view:: $(TARGET).pdf
	open $(TARGET).pdf

see:: $(TARGET).dvi
	xdvi $(TARGET)

%.eps: plots/%.plot
	gnuplot $< > figures/$@

%.eps: figures/%.fig
	fig2dev -L eps -p dummy $< $*.eps

spell::
	ispell *.tex

clean::
	rm -fv *.dvi *.aux *.log *~ *.bbl *.blg *.toc *.out *.ps *.pdf *.ent parsetab.py
	rm -fv $(addprefix figures/, $(addsuffix .eps, $(FIGURES)))

fresh::
	rm -fv *.dvi *.aux *.log *~ *.bbl *.blg *.toc *.ps *.pdf

distclean:: clean
	rm $(TARGET).ps
