# A Wikipedia Plain Text Extractor with Link Annotations 
## (mentions/anchors and their positions)  

This project is a simple wrapper around the Wikipedia Extractor by [Medialab](http://medialab.di.unipi.it/wiki/Wikipedia_Extractor).  
It generates a `JSON` object for each article. The JSON object contains the `id, title and plain text of the article, as well as annotations of article links in the text`.

We fork and modify this project to get a pre-training corpus from the Wikipedia dump

# 1. Input 
>  The input to be pre-processed is Wikipedia dump `enwiki-latest-pages-articles.xml.bz2`, which can be downloaded from [this](https://dumps.wikimedia.org/enwiki/20220301/enwiki-20220301-pages-articles.xml.bz2) or [this](https://dumps.wikimedia.org/enwiki/)


# 2. Usage

2.1 Unzip the Wikipedia dump to `enwiki-latest-pages-articles.xml` (about 81.5 GB)   
2.2 Convert the whole Wikipedia dump to plain text, use the following command:

	python annotated_wikiextractor.py -o extracted/
2.3 All options

	$ Usage:
	  annotated_wikiextractor.py [options]

    python annotated_wikiextractor.py --help

	Options:
	  -k, --keep-anchors    : do not drop annotations for anchor links (e.g. Anarchism#gender)
	  -c, --compress        : compress output files using bzip2 algorithm
	  -b ..., --bytes=...   : put specified bytes per output file (500K by default)
	  -o ..., --output=...  : place output files in specified directory (current
	                          directory by default)
	  --help                : display this help and exit
	  --usage               : display script usage


# 3. Output

3.1 JSON of a single article

	{"url": "http://en.wikipedia.org/wiki/Anarchism", 
	 "text": "Anarchism.\nAnarchism is a political philosophy which considers the state 
		undesirable, unnecessary and harmful, and instead promotes a stateless society, or 
		anarchy. It seeks to diminish ...", 
	 "id": 12, 
	 "annotations": [
		{"offset": 46, "uri": "Political_philosophy", "surface_form": "political philosophy"}, 
		{"offset": 72, "uri": "State_(polity)", "surface_form": "state"}, 
		{"offset": 163, "uri": "Anarchy", "surface_form": "anarchy"}, 
		...
	]}


3.2 Annotations are stored in an ordered list. A single annotation has the following form:

	
* `offset`: start positon of the string
* `id`: Wikipedia/DBPedia article name
* `surface_form`: the label of the link in the text (what part of the text was linked), i.e., mention/anchor
* `uri`: the linked entity


