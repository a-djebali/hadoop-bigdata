# Big Data with Hadoop 

Here's some examples of Hadoop tools

# Map Reduce</h1>

### Simple word counter 

Count total chars, lines and words.

```python
from mrjob.job import MRJob

class MRWordFrequencyCount(MRJob):
  
  def mapper(self, _, line):
    yield "chars", len(line)
    yield "words", len(line.split())
    yield "lines", 1

  def reducer(self, key, values):
    yield key, sum(values)

if __name__ == '__main__':
  MRWordFrequencyCount.run()
```

Run

``$ python mr_word_count.py file``

Output

``
  "chars" 3654
  "lines" 123
  "words" 417
``

### Total movies rated by user

In this example we're trying to get all movies rated by each user using `MovieLens <http://grouplens.org/datasets/movielens/>` dataset

.. image:: imgs/demo.png

```python
from mrjob.job import MRJob

class MovieByUserCounter(MRJob):
  def mapper(self, key, line):
    (userID, movieID, rating, timestamp) = line.split('\t')
    yield userID, movieID

  def reducer(self, user, movies):
    numMovies = 0
    for movie in movies:
      numMovies = numMovies + 1

    yield user, numMovies

if __name__ == '__main__':
  MovieByUserCounter.run()
```

Run

``$ python MoviesByUser.py ml-100k/u.data``

Output 

``
  "938"   108
  "939"   49
  "94"    400
  "940"   107
  "941"   22
  "942"   79
  "943"   168
  "95"    278
  "96"    56
  "97"    63
  "98"    27
  "99"    136
``

# Other examples soon...