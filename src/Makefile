# LaTeX program
TEX   := xelatex

# .tex file to compile (no extension)
SRC   := thesis

# Output filename
OUT   := $(shell date "+%Y-%m-%d")_$(SRC).pdf

# PDF viewer (`evince` for Linux, `open` for OS X)
VIEW  := $(if $(shell uname|grep Linux), evince, open)

# Compiles a TeX file
define mkpdf
	$(TEX) $(SRC)
endef

all: $(OUT)
	bibtex --terse $(SRC)
	# compile twice to complete the TOC and refs 
	for i in {1..2}; do\
	    $(call mkpdf);\
	done
	mv $(SRC).pdf $(OUT)

# Does a single pass-thru
$(OUT):
	$(mkpdf)

# Open the PDF as a background process
debug: all
	$(VIEW) $(OUT)&

# Remove all generated-build files
clean:
	rm -f *.aux *.bbl *.blg *.log *.toc

# Remove the PDF
clobber: clean
	rm -f *.pdf

