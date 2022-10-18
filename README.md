# Bengali Sentence Similarity Measurement

A Python package for measuring the semantic similarity among sentences in the Bengali language. Users will provide a reference sentence and a list of target sentences as input; and optionally the similarity assessment approach _(Default: Cosine Similarity)_ and the maximum sequence length _(Default: 512)_. The length will be calculated in terms of the number of tokens using the WordPiece tokenizer. Currently, the maximum sequence length limit is 512. BenSim will perform [normalization](https://github.com/csebuetnlp/normalizer) on the input texts and extract the contextual embeddings of the reference sentence and target sentences through a [pre-trained BERT](https://github.com/sagorbrur/bangla-bert) model. The similarities will be measured between each of the sentence pairs by applying either [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance) or [Cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity) (based on the input parameter). Finally, this will return a list of similarity scores between the reference sentence and the target sentences. If the assessment method is `cosine`, the higher scores will denote higher similarity, and the opposite will be for `euclidean`.

### Setup from clone
1. Install [Pytorch](https://pytorch.org/get-started/locally/) on your virtual environment.
2. Clone this repo.
3. Run the following commands to install:
```bash
$ python setup.py bdist_wheel # to build
$ pip install -e .
```

### Setup from Git
```bash
$ pip install git+https://github.com/AbuUbaida/bensim
```

<!-- ## Developing Bangla BERT Similarity

To install Bangla BERT Similarity, along with the tools you need to develop and run tests, run the following in your virtual environment:

```bash
$ python setup.py bdist_wheel # to build
$ pip install -e .[dev]
``` -->

### Default Usage
For the first usage, it may take a while to download the pretrained BERT model on your system memory.
* Sample input (single target sentence):
```python
from bensim import similarity
score = similarity.score('তোমার সাথে দেখা হয়ে ভালো লাগলো।', 'আপনার সাথে দেখা হয়ে ভালো লাগলো।')
score
```
* Sample output:
```
array([0.83910286], dtype=float32)
```
* Sample input (list of target sentences):
```python
from bensim import similarity
score = similarity.scores('তোমার সাথে দেখা হয়ে ভালো লাগলো।', ['আপনার সাথে দেখা হয়ে ভালো লাগলো।', 'আপনার সাথে দেখা হয়ে ভালো লাগলো।'])
scores
```
* Sample output:
```
array([0.83910286, 0.83910286], dtype=float32)
```

### Limiting max sequence length
To limit the maximum sequence length, `max_seq` can be set upto 512. If not mentioned, the default value will be `512`.
* Sample input:
```python
from bensim import similarity
score = similarity.score('তোমার সাথে দেখা হয়ে ভালো লাগলো।', 'আপনার সাথে দেখা হয়ে ভালো লাগলো।' ,  max_seq = 10)
score
```
* Sample output:
```
array([0.763596], dtype=float32)
```

### Computing the Euclidean distance
To get the similarity based on Euclidean _(Lower means Higher similarity)_ distance, simply set `euclidean` for the `similarity_method`. The default will be `cosine` _(Higher means Higher similarity)_.
* Sample input:
```python
from bensim import similarity
score = similarity.score('তোমার সাথে দেখা হয়ে ভালো লাগলো।', 'আপনার সাথে দেখা হয়ে ভালো লাগলো।' ,  similarity_method = 'euclidean')
score
```
* Sample output:
```
array([8.81357], dtype=float32)
```

## References:
* [Normalizer](https://github.com/csebuetnlp/normalizer)
* [Bangla BERT](https://github.com/sagorbrur/bangla-bert)
* [Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance)
* [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity)
* [PyTorch](https://pytorch.org/get-started/locally/)
