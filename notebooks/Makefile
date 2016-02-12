NOTEBOOKS := $(patsubst %.ipynb,%.rst,$(wildcard *.ipynb))
notebooks: $(NOTEBOOKS)

%.rst: %.ipynb
	    jupyter nbconvert --to rst $<
