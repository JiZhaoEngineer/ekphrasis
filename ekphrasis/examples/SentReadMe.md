## Sentiment Analysis Example

```python
from ekphrasis.classes.preprocessor import TextPreProcessor
from ekphrasis.classes.tokenizer import SocialTokenizer
from ekphrasis.utils.nlp import polarity

sentences = [
    "So there is no way for me to plug it in here in the US unless I go by a converter.",
    "Good case, Excellent value.",
    "Works great!",
    'The design is very odd, as the ear "clip" is not very comfortable at all.',
    "Needless to say, I wasted my money."
]

# define preprocessing pipeline
text_processor = TextPreProcessor(
    fix_text=True,
    unpack_contractions=True,
    tokenizer=SocialTokenizer(lowercase=True).tokenize,
)

# pass each sentence through the pipeline
tokenized_sentences = list(text_processor.pre_process_docs(sentences))
for sent in tokenized_sentences:
    _polarity, _scores = polarity(sent)
    print("{:.4f}\t".format(_polarity) + " ".join(sent))
```

#### Output

```shell
0.0139	so there is no way for me to plug it in here in the us unless i go by a converter .
0.3750	good case , excellent value .
0.0000	works great !
0.0500	the design is very odd , as the ear " clip " is not very comfortable at all .
0.0500	needless to say , i wasted my money .
```