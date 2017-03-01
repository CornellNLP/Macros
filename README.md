Cornell LaTeX Macro Dataset
==============================================

The dataset is available at: http://zissou.infosci.cornell.edu/data/MacroDataset.zip

This dataset contains a collection of LaTeX macro usages on arXiv [1], from July 1991 to September 2015 (Data was downloaded in November 2015).
For each macro definition in the LaTeX sources submitted to arXiv, we include the name and body of the macro, in addition to the arXiv tag of the paper, date of the submission and a list of authors of the paper.

The datasets contains 2,586,540 unique macro bodies, used 22,628,300 times (with a total of 1,198,870 names) in 583,079 papers.


URL: http://github.com/CornellNLP/Macros

Authors: Rahmtin Rotabi, 
		 Cristian Danescu-Niculescu-Mizil and 
		 Jon Kleinberg
		 
Contact: Rahmtin Rotabi <rahmtin@cs.cornell.edu>

Last updated: February 23, 2017

Version: 1.0

The dataset is further described in our paper:
	[Competition and Selection Among Conventions](https://arxiv.org/pdf/1702.06527.pdf)
	Rahmtin Rotabi, Cristian Danescu-Niculescu-Mizil, Jon Kleinberg
	Proceedings of WWW, 2017.

Files
-----

* arxiv_macro_data_release.txt - a txt file containing the macros
* README.md - this readme
* PythonScript.py - a simple python script that reads the data
* competing_conventions.pdf - The paper that used this dataset first


LaTeX macro description
------------------

In writing the LaTeX source for a paper, authors will often define one or more macros as a way to make the writing of the paper easier and more modular.
Each instance of a macro instance is specified by a name and a body definition which defines the functionality of the macro. 
Each time the formatting software for the paper sees the name of the macro, it replaces it with the body of the macro in the text.


Format
------

The dataset is a text file with the following format:
For each macro instance included in our dataset there is a block of lines followed by a blank line:
* First line: macro body
* Second line: macro name
* Third line: arXiv submission tag
* Fourth line: month of the the submission (MM YYYY)
* Fifth line and on:  author names (ordered)

Example:
```
macro_body: \text{\unslant[-.18]\delta}
macro_name: \mdelta
paper_id: 1507.00003
date: 07 2015
author: grozdanov,s.
author: lucas,a.
author: sachdev,s.
author: schalm,k.
```

The arXiv submission page can be accessed through (https://arxiv.org/abs/ + "paper_id") which in the case of this example is: https://arxiv.org/abs/1507.00003.
This submission was made in July 2015 and has 4 authors.


Sample Python script
----------
This script can also be found in the distributed zip file.

```python
def parse_data(filename):
    parsed_data = []
    with open(filename, 'r') as fin:
        current = {'authors': []}
        for line in fin:
            stripped = line.strip()
            if not stripped:
                parsed_data.append(current)
                current = {'authors': []}
            elif stripped.startswith('macro_body'):
                current['macro_body'] = stripped[len('macro_body')+2:]
            elif stripped.startswith('macro_name'):
                current['macro_name'] = stripped[len('macro_name')+2:]
            elif stripped.startswith('paper_id'):
                current['paper_id'] = stripped[len('paper_id')+2:]
            elif stripped.startswith('date'):
                current['date'] = stripped[len('date')+2:]
            elif stripped.startswith('author'):
                current['authors'].append(stripped[len('author')+2:])
    return parsed_data
```


References
----------

[1] http://www.arxiv.org/
