## Welcome to GitHub Pages



<!DOCTYPE html>
<html>
  <head>
    <title>A Visual Intro to NumPy and Data Representation – Jay Alammar – Visualizing machine learning one concept at a time</title>

        <meta charset="utf-8" />
    <meta content='text/html; charset=utf-8' http-equiv='Content-Type'>
    <meta http-equiv='X-UA-Compatible' content='IE=edge'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0'>

    
    <meta name="description" content="Discussions:
Hacker News (366 points, 21 comments), Reddit r/MachineLearning (256 points, 18 comments)


Translations: Chinese 1, Chinese 2, Japanese


  
  


The NumPy package is the workhorse of data analysis, machine learning, and scientific computing in the python ecosystem. It vastly simplifies manipulating and crunching vectors and matrices. Some of python’s leading package rely on NumPy as a fundamental piece of their infrastructure (examples include scikit-learn, SciPy, pandas, and tensorflow). Beyond the ability to slice and dice numeric data, mastering numpy will give you an edge when dealing and debugging with advanced usecases in these libraries.

In this post, we’ll look at some of the main ways to use NumPy and how it can represent different types of data (tables, images, text…etc) before we can serve them to machine learning models.

" />
    <meta property="og:description" content="Discussions:
Hacker News (366 points, 21 comments), Reddit r/MachineLearning (256 points, 18 comments)


Translations: Chinese 1, Chinese 2, Japanese


  
  


The NumPy package is the workhorse of data analysis, machine learning, and scientific computing in the python ecosystem. It vastly simplifies manipulating and crunching vectors and matrices. Some of python’s leading package rely on NumPy as a fundamental piece of their infrastructure (examples include scikit-learn, SciPy, pandas, and tensorflow). Beyond the ability to slice and dice numeric data, mastering numpy will give you an edge when dealing and debugging with advanced usecases in these libraries.

In this post, we’ll look at some of the main ways to use NumPy and how it can represent different types of data (tables, images, text…etc) before we can serve them to machine learning models.

" />
    
    <meta name="author" content="Jay Alammar" />

    
    <meta property="og:title" content="A Visual Intro to NumPy and Data Representation" />
    <meta property="twitter:title" content="A Visual Intro to NumPy and Data Representation" />
    

    <!--[if lt IE 9]>
      <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
    <![endif]-->

    <script src="/js/jquery-3.1.1.slim.min.js"></script>
    <script type="text/javascript" src="/js/d3.min.js"></script>
    <script type="text/javascript" src="/js/d3-selection-multi.v0.4.min.js"></script>
    <script type="text/javascript" src="/js/d3-jetpack.js"></script>

    <link rel="stylesheet" href="/css/bootstrap.min.css" />
    <link rel="stylesheet" href="/css/bootstrap-theme.min.css" />
    <script src="/js/bootstrap.min.js" > </script>

    <link rel="stylesheet" type="text/css" href="/bower_components/jquery.gifplayer/dist/gifplayer.css"/>
    <script type="text/javascript" src="/bower_components/jquery.gifplayer/dist/jquery.gifplayer.js"></script>

    <!--
    <script data-main="scripts/main" src="scripts/require.js"></script>
    -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.css" integrity="sha384-wE+lCONuEo/QSfLb4AfrSk7HjWJtc4Xc1OiB2/aDBzHzjnlBP4SX7vjErTcwlA8C" crossorigin="anonymous">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.js" integrity="sha384-tdtuPw3yx/rnUGmnLNWXtfjb9fpmwexsd+lr6HUYnUY4B7JhB5Ty7a1mYd+kto/s" crossorigin="anonymous"></script>

    <link rel="stylesheet" type="text/css" href="/style.css" />
    <link rel="alternate" type="application/rss+xml" title="Jay Alammar - Visualizing machine learning one concept at a time" href="/feed.xml" />

    <meta name="viewport" content="width=device-width">
    <!-- Created with Jekyll Now - http://github.com/barryclark/jekyll-now -->

    <!-- Piwik -->
    <!-- Piwik
    <script type="text/javascript">
        var _paq = _paq || [];
        _paq.push(["setDomains", ["*.example.org"]]);
        _paq.push(['trackPageView']);
        _paq.push(['enableLinkTracking']);
        (function() {
            var u="https://a.jalammar.com/";
            _paq.push(['setTrackerUrl', u+'piwik.php']);
            _paq.push(['setSiteId', '1']);
            var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0];
            g.type='text/javascript'; g.async=true; g.defer=true; g.src=u+'piwik.js'; s.parentNode.insertBefore(g,s);
        })();
    </script>
    <noscript><p><img src="https://a.jalammar.com/piwik.php?idsite=1" style="border:0;" alt="" /></p></noscript>-->
    <!-- End Piwik Code -->

    <!-- End Piwik Code -->
  </head>

  <body>
    <div class="wrapper-masthead">
      <div class="container">
        <header class="masthead clearfix">
          <a href="/" class="site-avatar"><img src="https://avatars0.githubusercontent.com/u/1007956?s=460&v=4" /></a>

          <div class="site-info">
            <h1 class="site-name"><a href="/">Jay Alammar</a></h1>
            <p class="site-description">Visualizing machine learning one concept at a time</p>
          </div>

          <nav>
            <a href="/">Blog</a>
            <a href="/about">About</a>
          </nav>
        </header>
      </div>
    </div>

    <div id="main" role="main" class="container">
      <article class="post">
  <h1>A Visual Intro to NumPy and Data Representation</h1>

  <div class="entry prediction">
    <p><span class="discussion">Discussions:
<a href="https://news.ycombinator.com/item?id=20282985" class="hn-link">Hacker News (366 points, 21 comments)</a>, <a href="https://www.reddit.com/r/MachineLearning/comments/c5nc89/p_a_visual_intro_to_numpy_and_data_representation/" class="">Reddit r/MachineLearning (256 points, 18 comments)</a>
</span>
<br />
<span class="discussion">Translations: <a href="http://www.junphy.com/wordpress/index.php/2019/10/24/visual-numpy/">Chinese 1</a>, <a href="https://github.com/kevingo/blog/blob/master/ML/visual-numpy.md">Chinese 2</a>, <a href="https://note.mu/sayajewels/n/n95edaedb0fc5">Japanese</a></span></p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array.png" />
  <br />
</div>

<p>The <a href="https://www.numpy.org/">NumPy</a> package is the workhorse of data analysis, machine learning, and scientific computing in the python ecosystem. It vastly simplifies manipulating and crunching vectors and matrices. Some of python’s leading package rely on NumPy as a fundamental piece of their infrastructure (examples include scikit-learn, SciPy, pandas, and tensorflow). Beyond the ability to slice and dice numeric data, mastering numpy will give you an edge when dealing and debugging with advanced usecases in these libraries.</p>

<p>In this post, we’ll look at some of the main ways to use NumPy and how it can represent different types of data (tables, images, text…etc) before we can serve them to machine learning models.</p>

<!--more-->

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="n">np</span>
</code></pre></div></div>

<h2 id="creating-arrays">Creating Arrays</h2>

<p>We can create a NumPy array (a.k.a. the mighty <a href="https://docs.scipy.org/doc/numpy/reference/arrays.ndarray.html">ndarray</a>) by passing a python list to it and using ` np.array()`. In this case, python creates the array we can see on the right here:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/create-numpy-array-1.png" />
  <br />
</div>

<p>There are often cases when we want NumPy to initialize the values of the array for us. NumPy provides methods like ones(), zeros(), and random.random() for these cases. We just pass them the number of elements we want it to generate:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/create-numpy-array-ones-zeros-random.png" />
  <br />
</div>

<p>Once we’ve created our arrays, we can start to manipulate them in interesting ways.</p>

<h2 id="array-arithmetic">Array Arithmetic</h2>
<p>Let’s create two NumPy arrays to showcase their usefulness. We’ll call them <code class="language-plaintext highlighter-rouge">data</code> and <code class="language-plaintext highlighter-rouge">ones</code>:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-arrays-example-1.png" />
  <br />
</div>

<p><br /></p>

<p>Adding them up position-wise (i.e. adding the values of each row) is as simple as typing <code class="language-plaintext highlighter-rouge">data + ones</code>:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-arrays-adding-1.png" />
  <br />
</div>

<p><br /></p>

<p>When I started learning such tools, I found it refreshing that an abstraction like this makes me not have to program such a calculation in loops. It’s a wonderful abstraction that allows you to think about problems at a higher level.</p>

<p>And it’s not only addition that we can do this way:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array-subtract-multiply-divide.png" />
  <br />
</div>

<p><br /></p>

<p>There are often cases when we want to carry out an operation between an array and a single number (we can also call this an operation between a vector and a scalar). Say, for example, our array represents distance in miles, and we want to convert it to kilometers. We simply say <code class="language-plaintext highlighter-rouge">data * 1.6</code>:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array-broadcast.png" />
  <br />
</div>

<p><br /></p>

<p>See how NumPy understood that operation to mean that the multiplication should happen with each cell? That concept is called <em>broadcasting</em>, and it’s very useful.</p>

<h2 id="indexing">Indexing</h2>

<p>We can index and slice NumPy arrays in all the ways we can slice python lists:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array-slice.png" />
  <br />
</div>

<h2 id="aggregation">Aggregation</h2>

<p>Additional benefits NumPy gives us are aggregation functions:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array-aggregation.png" />
  <br />
</div>

<p>In addition to <code class="language-plaintext highlighter-rouge">min</code>, <code class="language-plaintext highlighter-rouge">max</code>, and <code class="language-plaintext highlighter-rouge">sum</code>, you get all the greats like <code class="language-plaintext highlighter-rouge">mean</code> to get the average, <code class="language-plaintext highlighter-rouge">prod</code> to get the result of multiplying all the elements together, <code class="language-plaintext highlighter-rouge">std</code> to get standard deviation, and <a href="https://jakevdp.github.io/PythonDataScienceHandbook/02.04-computation-on-arrays-aggregates.html">plenty of others</a>.</p>

<h2 id="in-more-dimensions">In more dimensions</h2>

<p>All the examples we’ve looked at deal with vectors in one dimension. A key part of the beauty of NumPy is its ability to apply everything we’ve looked at so far to any number of dimensions.</p>

<h3 id="creating-matrices">Creating Matrices</h3>

<p>We can pass python lists of lists in the following shape to have NumPy create a matrix to represent them:</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([[</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">],[</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">]])</span>
</code></pre></div></div>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-array-create-2d.png" />
  <br />
</div>

<p>We can also use the same methods we mentioned above (<code class="language-plaintext highlighter-rouge">ones()</code>, <code class="language-plaintext highlighter-rouge">zeros()</code>, and <code class="language-plaintext highlighter-rouge">random.random()</code>) as long as we give them a tuple describing the dimensions of the matrix we are creating:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-ones-zeros-random.png" />
  <br />
</div>

<p><br /></p>

<h3 id="matrix-arithmetic">Matrix Arithmetic</h3>

<p>We can add and multiply matrices using arithmetic operators (<code class="language-plaintext highlighter-rouge">+-*/</code>) if the two matrices are the same size. NumPy handles those as position-wise operations:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-arithmetic.png" />
  <br />
</div>

<p><br /></p>

<p>We can get away with doing these arithmetic operations on matrices of different size only if the different dimension is one (e.g. the matrix has only one column or one row), in which case NumPy uses its broadcast rules for that operation:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-broadcast.png" />
  <br />
</div>

<p><br /></p>

<h3 id="dot-product">Dot Product</h3>

<p>A key distinction to make with arithmetic is the case of <a href="https://www.mathsisfun.com/algebra/matrix-multiplying.html">matrix multiplication</a> using the dot product. NumPy gives every matrix a <code class="language-plaintext highlighter-rouge">dot()</code> method we can use to carry-out dot product operations with other matrices:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-dot-product-1.png" />
  <br />
</div>

<p><br /></p>

<p>I’ve added matrix dimensions at the bottom of this figure to stress that the two matrices have to have the same dimension on the side they face each other with. You can visualize this operation as looking like this:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-dot-product-2.png" />
  <br />
</div>

<p><br />
<br /></p>

<h3 id="matrix-indexing">Matrix Indexing</h3>

<p>Indexing and slicing operations become even more useful when we’re manipulating matrices:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-indexing.png" />
  <br />
</div>

<p><br /></p>

<h3 id="matrix-aggregation">Matrix Aggregation</h3>

<p>We can aggregate matrices the same way we aggregated vectors:</p>
<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-aggregation-1.png" />
  <br />
</div>

<p><br /></p>

<p>Not only can we aggregate all the values in a matrix, but we can also aggregate across the rows or columns by using the <code class="language-plaintext highlighter-rouge">axis</code> parameter:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-matrix-aggregation-4.png" />
  <br />
</div>

<p><br /></p>

<h2 id="transposing-and-reshaping">Transposing and Reshaping</h2>

<p>A common need when dealing with matrices is the need to rotate them. This is often the case when we need to take the dot product of two matrices and need to align the dimension they share. NumPy arrays have a convenient property called <code class="language-plaintext highlighter-rouge">T</code> to get the transpose of a matrix:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-transpose.png" />
  <br />
</div>

<p><br /></p>

<p>In more advanced use case, you may find yourself needing to switch the dimensions of a certain matrix. This is often the case in machine learning applications where a certain model expects a certain shape for the inputs that is different from your dataset. NumPy’s <code class="language-plaintext highlighter-rouge">reshape()</code> method is useful in these cases. You just pass it the new dimensions you want for the matrix. You can pass -1 for a dimension and NumPy can infer the correct dimension based on your matrix:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-reshape.png" />
  <br />
</div>

<p><br /></p>

<h2 id="yet-more-dimensions">Yet More Dimensions</h2>
<p>NumPy can do everything we’ve mentioned in any number of dimensions. Its central data structure is called ndarray (N-Dimensional Array) for a reason.</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-3d-array.png" />
  <br />
</div>

<p>In a lot of ways, dealing with a new dimension is just adding a comma to the parameters of a NumPy function:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-3d-array-creation.png" />
  <br />
</div>

<p>Note: Keep in mind that when you print a 3-dimensional NumPy array, the text output visualizes the array differently than shown here.  NumPy’s order for printing n-dimensional arrays is that the last axis is looped over the fastest, while the first is the slowest. Which means that <code class="language-plaintext highlighter-rouge">np.ones((4,3,2))</code> would be printed as:</p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">array</span><span class="p">([[[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">]],</span>

       <span class="p">[[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">]],</span>

       <span class="p">[[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">]],</span>

       <span class="p">[[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">],</span>
        <span class="p">[</span><span class="mf">1.</span><span class="p">,</span> <span class="mf">1.</span><span class="p">]]])</span>
</code></pre></div></div>

<h2 id="practical-usage">Practical Usage</h2>

<p>And now for the payoff. Here are some examples of the useful things NumPy will help you through.</p>

<h3 id="formulas">Formulas</h3>
<p>Implementing mathematical formulas that work on matrices and vectors is a key use case to consider NumPy for. It’s why NumPy is the darling of the scientific python community. For example, consider the mean square error formula that is central to supervised machine learning models tackling regression problems:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/mean-square-error-formula.png" />
  <br />
</div>

<p><br /></p>

<p>Implementing this is a breeze in NumPy:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-mean-square-error-formula.png" />
  <br />
</div>

<p><br /></p>

<p>The beauty of this is that numpy does not care if <code class="language-plaintext highlighter-rouge">predictions</code> and <code class="language-plaintext highlighter-rouge">labels</code> contain one or a thousand values (as long as they’re both the same size). We can walk through an example stepping sequentially through the four operations in that line of code:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-mse-1.png" />
  <br />
</div>

<p><br /></p>

<p>Both the predictions and labels vectors contain three values. Which means n has a value of three. After we carry out the subtraction, we end up with the values looking like this:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-mse-2.png" />
  <br />
</div>

<p><br /></p>

<p>Then we can square the values in the vector:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-mse-3.png" />
  <br />
</div>

<p><br /></p>

<p>Now we sum these values:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-mse-4.png" />
  <br />
</div>

<p><br /></p>

<p>Which results in the error value for that prediction and a score for the quality of the model.</p>

<h3 id="data-representation">Data Representation</h3>

<p>Think of all the data types you’ll need to crunch and build models around (spreadsheets, images, audio…etc). So many of them are perfectly suited for representation in an n-dimensional array:</p>

<h4 id="tables-and-spreadsheets">Tables and Spreadsheets</h4>
<ul>
  <li>A spreadsheet or a table of values is a two dimensional matrix. Each sheet in a spreadsheet can be its own variable. The most popular abstraction in python for those is the <a href="/gentle-visual-intro-to-data-analysis-python-pandas/">pandas dataframe</a>, which actually uses NumPy and builds on top of it.</li>
</ul>

<div class="img-div-any-width">
   <image src="/images/pandas-intro/0%20excel-to-pandas.png" />
   <br />
 </div>

<h4 id="audio-and-timeseries">Audio and Timeseries</h4>
<ul>
  <li>An audio file is a one-dimensional array of samples. Each sample is a number representing a tiny chunk of the audio signal. CD-quality audio may have 44,100 samples per second and each sample is an integer between -32767 and 32768. Meaning if you have a ten-seconds WAVE file of CD-quality, you can load it in a NumPy array with length 10 * 44,100 = 441,000 samples. Want to extract the first second of audio? simply load the file into a NumPy array that we’ll call <code class="language-plaintext highlighter-rouge">audio</code>, and get <code class="language-plaintext highlighter-rouge">audio[:44100]</code>.</li>
</ul>

<p>Here’s a look at a slice of an audio file:</p>

<div class="img-div-any-width">
    <image src="/images/numpy/numpy-audio.png" />
    <br />
  </div>

<p>The same goes for time-series data (for example, the price of a stock over time).</p>

<h4 id="images">Images</h4>
<ul>
  <li>
    <p>An image is a matrix of pixels of size (height x width).</p>

    <ul>
      <li>If the image is black and white (a.k.a. grayscale), each pixel can be represented by a single number (commonly between 0 (black) and 255 (white)). Want to crop the top left 10 x 10 pixel part of the image? Just tell NumPy to get you <code class="language-plaintext highlighter-rouge">image[:10,:10]</code>.</li>
    </ul>
  </li>
</ul>

<p>Here’s a look at a slice of an image file:</p>

<div class="img-div-any-width">
   <image src="/images/numpy/numpy-grayscale-image.png" />
   <br />
 </div>

<ul>
  <li>
    <p>If the image is colored, then each pixel is represented by three numbers - a value for each of red, green, and blue. In that case we need a 3rd dimension (because each cell can only contain one number). So a colored image is represented by an ndarray of dimensions: (height x width x 3).</p>

    <div class="img-div-any-width">
     <image src="/images/numpy/numpy-color-image.png" />
     <br />
   </div>
  </li>
</ul>

<h4 id="language">Language</h4>
<p>If we’re dealing with text, the story is a little different. The numeric representation of text requires a step of building a vocabulary (an inventory of all the unique words the model knows) and an <a href="/illustrated-word2vec/">embedding step</a>. Let us see the steps of numerically representing this (translated) quote by an ancient spirit:</p>

<p>“Have the bards who preceded me left any theme unsung?”</p>

<p>A model needs to look at a large amount of text before it can numerically represent the anxious words of this warrior poet. We can proceed to have it process a <a href="http://mattmahoney.net/dc/textdata.html">small dataset</a> and use it to build a vocabulary (of 71,290 words):</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-nlp-vocabulary.png" />
  <br />
</div>

<p>The sentence can then be broken into an array of tokens (words or parts of words based on common rules):</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-nlp-tokenization.png" />
  <br />
</div>

<p>We then replace each word by its id in the vocabulary table:</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-nlp-ids.png" />
  <br />
</div>

<p>These ids still don’t provide much information value to a model. So before feeding a sequence of words to a model, the tokens/words need to be replaced with their embeddings (50 dimension <a href="/illustrated-word2vec/">word2vec embedding</a> in this case):</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-nlp-embeddings.png" />
  <br />
</div>

<p>You can see that this NumPy array has the dimensions [embedding_dimension x sequence_length]. In practice these would be the other way around, but I’m presenting it this way for visual consistency. For performance reasons, deep learning models tend to preserve the first dimension for batch size (because the model can be trained faster if multiple examples are trained in parallel). This is a clear case where <code class="language-plaintext highlighter-rouge">reshape()</code> becomes super useful. A model like <a href="/illustrated-bert/">BERT</a>, for example, would expect its inputs in the shape: [batch_size, sequence_length, embedding_size].</p>

<div class="img-div-any-width">
  <image src="/images/numpy/numpy-nlp-bert-shape.png" />
  <br />
</div>

<p>This is now a numeric volume that a model can crunch and do useful things with. I left the other rows empty, but they’d be filled with other examples for the model to train on (or predict).</p>

<p>(It turned out the <a href="https://en.wikisource.org/wiki/The_Poem_of_Antara">poet’s words</a> in our example were immortalized more so than those of the other poets which trigger his anxieties. Born a slave owned by his father, <a href="https://en.wikipedia.org/wiki/Antarah_ibn_Shaddad">Antarah’s</a> valor and command of language gained him his freedom and the mythical status of having his poem as one of <a href="https://en.wikipedia.org/wiki/Mu%27allaqat">seven poems suspended in the kaaba</a> in pre-Islamic Arabia).</p>

  </div>

  <div class="date">
    Written on June 26, 2019
  </div>

  
</article>

    </div>



    <!-- Begin Mailchimp Signup Form -->
    <link href="//cdn-images.mailchimp.com/embedcode/classic-10_7.css" rel="stylesheet" type="text/css">
    <style type="text/css">
    	#mc_embed_signup{background:#fff; clear:left; font:14px Helvetica,Arial,sans-serif; }
    	/* Add your own Mailchimp form style overrides in your site stylesheet or in this style block.
    	   We recommend moving this block and the preceding CSS link to the HEAD of your HTML file. */
    </style>
    <div id="mc_embed_signup">
    <form action="https://github.us19.list-manage.com/subscribe/post?u=2a4ade7dafcdbbf2eb4aae3cf&amp;id=f1f8c03f13" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
        <div id="mc_embed_signup_scroll">
    	<h2>Subscribe to get notified about upcoming posts by email</h2>
    <div class="mc-field-group">
    	<label for="mce-EMAIL">Email Address </label>
    	<input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL">
    </div>
    	<div id="mce-responses" class="clear">
    		<div class="response" id="mce-error-response" style="display:none"></div>
    		<div class="response" id="mce-success-response" style="display:none"></div>
    	</div>    <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
        <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_2a4ade7dafcdbbf2eb4aae3cf_f1f8c03f13" tabindex="-1" value=""></div>
        <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
        </div>
    </form>
    </div>
    <script type='text/javascript' src='//s3.amazonaws.com/downloads.mailchimp.com/js/mc-validate.js'></script><script type='text/javascript'>(function($) {window.fnames = new Array(); window.ftypes = new Array();fnames[0]='EMAIL';ftypes[0]='email';fnames[1]='FNAME';ftypes[1]='text';fnames[2]='LNAME';ftypes[2]='text';fnames[3]='ADDRESS';ftypes[3]='address';fnames[4]='PHONE';ftypes[4]='phone';fnames[5]='BIRTHDAY';ftypes[5]='birthday';}(jQuery));var $mcj = jQuery.noConflict(true);</script>
    <!--End mc_embed_signup-->

<div style="padding: 10px 0 10px 3%; color: #555; font-size:85%">
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

<br/>
Attribution example:
<br/>
<i>Alammar, Jay (2018). The Illustrated Transformer [Blog post]. Retrieved from <a href="https://jalammar.github.io/illustrated-transformer/">https://jalammar.github.io/illustrated-transformer/</a></i>

<br/><br/>
Note: If you translate any of the posts, let me know so I can link your translation to the original post. My email is in the <a href="/about">about page</a>.
</div>


    <div class="wrapper-footer">
      <div class="container">
        <footer class="footer">
          



<a href="https://github.com/jalammar"><i class="svg-icon github"></i></a>

<a href="https://www.linkedin.com/in/jalammar"><i class="svg-icon linkedin"></i></a>


<a href="https://www.twitter.com/jalammar"><i class="svg-icon twitter"></i></a>



        </footer>
      </div>
    </div>

    
	<!-- Google Analytics -->
	<script>
		(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
		(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
		m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
		})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

		ga('create', 'UA-71956058-1', 'auto');
		ga('send', 'pageview', {
		  'page': '/visual-numpy/',
		  'title': 'A Visual Intro to NumPy and Data Representation'
		});
	</script>
	<!-- End Google Analytics -->


  </body>
</html>
