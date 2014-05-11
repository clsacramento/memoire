
LANG=french
LOGO=logo-fc.jpg logo-cnam.png
SRC = couverture-ebt.tex ebt.tex intro.tex chap1.tex chap2.tex chap3.tex concl.tex ann1.tex
BIB = biblio.bib
PDF = couverture-ebt.pdf ebt.pdf
EBT = ebt
MEM = mem
REP := $(shell basename $(shell pwd))

# make -B pour forcer une regénération complète

# convertir le fichier biblio s'il contient des caractères utf8
#  recode -d u8..ltex biblio.bib
# n'est plus nécessaire avec biber

%.ind : %.idx
	texindy -v -L $(LANG) -M lang/$(LANG)/utf8 -I latex $<

%.pdf : %.tex
	pdflatex $<

all : $(PDF)

$(EBT).pdf : $(SRC)
	pdflatex $(EBT).tex
#	bibtex $(EBT)
	biber $(EBT)
	texindy -v -L $(LANG) -M lang/$(LANG)/utf8 -I latex $(EBT).idx
	makeglossaries $(EBT)
	pdflatex $(EBT).tex
	pdflatex $(EBT).tex

tar :
	tar cvzf $(EBT).tgz -C .. $(REP)/Makefile $(SRC:%=$(REP)/%) $(BIB:%=$(REP)/%) $(LOGO:%=$(REP)/%)

clean :
	-rm -f *.aux *.log *.out *.lof *.lot *.toc *.ind *.idx *.ilg *.blg *.bbl *.bcf \
	*.acn *.alg *.acr *.glg *.gls *.glo *.xdy *.run.xml *-blx.bib

proper: clean
	-rm -f $(PDF)
