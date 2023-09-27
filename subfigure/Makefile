PACKAGE = subfigure
########################################################################
## LaTeX2e Makefile
##
## Update the following defines for your local configuration, 
##
CONTRIB   = /usr/local/lib/texmf/tex/subfigure
##
A2PS      = a2ps
CP        = cp	
DVIPS     = dvips -t letter
GZIP      = gzip
LATEX	  = latex
MAKEINDEX = makeindex
PDFLATEX  = pdflatex
PS2PDF    = ps2pdf
RM        = rm
TAR       = tar
########################################################################
## make [all]         Generates the style (.sty) file, the doc and 
##                      test files (.ps) and cleans up the directory.
## make [un]install 	Install or uninstall the style (.sty) file from
##			  the CONTRIB area.
## make [very]clean	Clean out various auxillary files.  "veryclean"
##			  cleans out more stuff.
########################################################################
## make dvi		Generate the *.dvi version of the documentation.
## make [full]ps	Generate the documentation.  The "fullps" version
##			  adds the change log and the cross-references.
## make idx		Generate the change log and the cross-references
##			  (for fullps -- requires MAKEINDEX).
## make sty		Generate the style (.sty) file.
## make pdf		Generate the *.pdf version of the documentation.
########################################################################
## make test		Runs test program(s).
## make distribtion	Builds a distribution (.tar.gz) file.
########################################################################

all:		pdf test clean

install:	sty
		$(CP) $(PACKAGE).sty $(CONTRIB)
uninstall:	; -$(RM) -f $(CONTRIB)/$(PACKAGE).sty
clean:	        ; -$(RM) -f *.dvi *.log *.aux *.lof *.lot *.lom *.toc 
		-$(RM) -f *.idx *.ind *.glo *.gls *.ilg *.out *~
veryclean:	clean
		-$(RM) -f *.sty *.cls *.ps *.pdf *.gz *pk ltxdoc.cfg

dvi:		$(PACKAGE).dvi
fullps:		dvi idx ps
idx:		$(PACKAGE).ind $(PACKAGE).gls
		$(LATEX) $(PACKAGE).dtx
		$(LATEX) $(PACKAGE).dtx
ps:		$(PACKAGE).ps
sty:		$(PACKAGE).sty
pdf:		fullps
		$(PS2PDF) $(PACKAGE).ps > $(PACKAGE).pdf

test:		test1 test2 test3 test4 test5

distribution:	; mkdir $(PACKAGE)
		$(CP) -p README Makefile $(PACKAGE).pdf $(PACKAGE)
		$(CP) -p $(PACKAGE).dtx $(PACKAGE).ins $(PACKAGE)
		$(CP) -p test*.tex $(PACKAGE)
		$(TAR) -cvf $(PACKAGE).tar ./$(PACKAGE) 
		$(RM) -rf $(PACKAGE)
		$(GZIP) -9 $(PACKAGE).tar

$(PACKAGE).aux:	$(PACKAGE).dtx $(PACKAGE).sty
		$(LATEX) $(PACKAGE).dtx
		$(LATEX) $(PACKAGE).dtx

$(PACKAGE).dvi:	$(PACKAGE).dtx $(PACKAGE).sty $(PACKAGE).aux
		$(LATEX) $(PACKAGE).dtx
		$(LATEX) $(PACKAGE).dtx
		$(LATEX) $(PACKAGE).dtx

$(PACKAGE).glo:	$(PACKAGE).dtx $(PACKAGE).sty
		$(LATEX) $(PACKAGE).dtx

$(PACKAGE).gls:	$(PACKAGE).glo
		-$(MAKEINDEX) -s gglo.ist -o $(PACKAGE).gls $(PACKAGE).glo

$(PACKAGE).idx:	$(PACKAGE).dtx $(PACKAGE).sty
		$(LATEX) $(PACKAGE).dtx

$(PACKAGE).ind:	$(PACKAGE).idx
		-$(MAKEINDEX) -s gind.ist $(PACKAGE).idx

$(PACKAGE).ps:	$(PACKAGE).dvi
		$(DVIPS) -o $(PACKAGE).ps $(PACKAGE).dvi

$(PACKAGE).sty:	$(PACKAGE).dtx $(PACKAGE).ins 
		$(LATEX) $(PACKAGE).ins

test1:		$(PACKAGE).sty
		$(LATEX) test.tex
		$(LATEX) test.tex
		$(LATEX) test.tex
		$(DVIPS) -o test.ps test.dvi

test2:		$(PACKAGE).sty
		$(LATEX) test2.tex
		$(LATEX) test2.tex
		$(DVIPS) -o test2.ps test2.dvi

test3:		$(PACKAGE).sty
		$(LATEX) test3.tex
		$(LATEX) test3.tex
		$(LATEX) test3.tex
		$(DVIPS) -o test3.ps test3.dvi

test4:		$(PACKAGE).sty
		$(PDFLATEX) test4.tex
		$(PDFLATEX) test4.tex
		$(PDFLATEX) test4.tex

test5:		$(PACKAGE).sty
		$(LATEX) test5.tex
		$(LATEX) test5.tex
		$(A2PS) -o test5a.ps test5.log
		$(DVIPS) -o test5b.ps test5.dvi

