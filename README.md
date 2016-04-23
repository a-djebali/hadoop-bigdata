# Big Data with Hadoop 

<ul>
  <li><a href="#mapreduce">Map Reduce</a></li>
  <ul>
    <li><a href="#example1">Total movies rated by user</a></li>
  </ul>
</ul>

<h1 id="mapreduce"></h1>
<h3 id="example1">Total movies rated by user</h3>
<p>In this example we're trying to get total movies rated by each user using <a href="http://grouplens.org/datasets/movielens/"> movielens</a> dataset</p>
<img src="imgs/demo.png">
<pre>
  <code>
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
  </code>
</pre>