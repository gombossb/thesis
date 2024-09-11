DOCUMENT=thesis
PREFIX = docker run --rm -v ./:/workdir registry.gitlab.com/islandoftex/images/texlive:TL2024-2024-09-08-full
#MODE=-interaction=batchmode

all: clean xelatex
	echo

xelatex: compile_xelatex
	$(PREFIX) mv $(DOCUMENT)-xelatex.pdf ../pdf/$(DOCUMENT).pdf

compile_xelatex:
	$(PREFIX) xelatex $(MODE) $(DOCUMENT)
	$(PREFIX) bibtex $(DOCUMENT)
	$(PREFIX) xelatex $(MODE) $(DOCUMENT)
	$(PREFIX) xelatex $(MODE) $(DOCUMENT)
	$(PREFIX) mv $(DOCUMENT).pdf $(DOCUMENT)-xelatex.pdf

pdflatex: compile_pdflatex
	$(PREFIX) mv $(DOCUMENT)-pdflatex.pdf ../pdf/$(DOCUMENT).pdf

compile_pdflatex:
	$(PREFIX) pdflatex $(MODE) $(DOCUMENT)
	$(PREFIX) bibtex $(DOCUMENT)
	$(PREFIX) pdflatex $(MODE) $(DOCUMENT)
	$(PREFIX) pdflatex $(MODE) $(DOCUMENT)
	$(PREFIX) mv $(DOCUMENT).pdf $(DOCUMENT)-pdflatex.pdf

lualatex: compile_lualatex
	$(PREFIX) mv $(DOCUMENT)-lualatex.pdf ../pdf/$(DOCUMENT).pdf

compile_lualatex:	
	$(PREFIX) lualatex $(MODE) $(DOCUMENT)
	$(PREFIX) bibtex $(DOCUMENT)
	$(PREFIX) lualatex $(MODE) $(DOCUMENT)
	$(PREFIX) lualatex $(MODE) $(DOCUMENT)
	$(PREFIX) mv $(DOCUMENT).pdf $(DOCUMENT)-lualatex.pdf

switch_to_hungarian:
	$(PREFIX) sed -i "s|^\\\input{include/thesis-en}|%\\\input{include/thesis-en}|" $(DOCUMENT).tex
	$(PREFIX) sed -i "s|^%\\\input{include/thesis-hu}|\\\input{include/thesis-hu}|" $(DOCUMENT).tex

test_hu:
	${MAKE} clean compile_xelatex
	${MAKE} clean compile_pdflatex
	${MAKE} clean compile_lualatex
	$(PREFIX) mv $(DOCUMENT)-xelatex.pdf ../pdf/$(DOCUMENT)-xelatex-hu.pdf
	$(PREFIX) mv $(DOCUMENT)-pdflatex.pdf ../pdf/$(DOCUMENT)-pdflatex-hu.pdf
	$(PREFIX) mv $(DOCUMENT)-lualatex.pdf ../pdf/$(DOCUMENT)-lualatex-hu.pdf

switch_to_english:
	$(PREFIX) sed -i "s|^\\\input{include/thesis-hu}|%\\\input{include/thesis-hu}|" $(DOCUMENT).tex
	$(PREFIX) sed -i "s|^%\\\input{include/thesis-en}|\\\input{include/thesis-en}|" $(DOCUMENT).tex

test_en:
	${MAKE} switch_to_english
	${MAKE} clean compile_xelatex
	${MAKE} clean compile_pdflatex
	${MAKE} clean compile_lualatex
	$(PREFIX) mv $(DOCUMENT)-xelatex.pdf ../pdf/$(DOCUMENT)-xelatex-en.pdf
	$(PREFIX) mv $(DOCUMENT)-pdflatex.pdf ../pdf/$(DOCUMENT)-pdflatex-en.pdf
	$(PREFIX) mv $(DOCUMENT)-lualatex.pdf ../pdf/$(DOCUMENT)-lualatex-en.pdf
	${MAKE} switch_to_hungarian

test: test_hu test_en
	echo

clean:
	echo Cleaning temporary files...
	$(PREFIX) rm -f *.aux *.dvi *.thm *.lof *.log *.lot *.fls *.out *.toc *.bbl *.blg
