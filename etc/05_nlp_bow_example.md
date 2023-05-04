---
layout: default
title: NLP BoW Example
nav_order: 5
parent: Etc
---

# 2) Bag of Words(BoW) Example(_21.12.08_)

ipynb 파일을 html로 변환한 내용입니다.

<div class="cell code" data-execution_count="9" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="scgYk1sHlr4R" data-outputId="4b1b5541-6ba5-4b54-a47a-22c2fb3a5262">
<div class="sourceCode" id="cb1"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="op">!</span>pip install konlpy</span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a><span class="op">!</span>pip install nltk</span></code></pre></div>
<div class="output stream stdout">
<pre><code>Requirement already satisfied: konlpy in /usr/local/lib/python3.7/dist-packages (0.5.2)
Requirement already satisfied: beautifulsoup4==4.6.0 in /usr/local/lib/python3.7/dist-packages (from konlpy) (4.6.0)
Requirement already satisfied: JPype1&gt;=0.7.0 in /usr/local/lib/python3.7/dist-packages (from konlpy) (1.3.0)
Requirement already satisfied: colorama in /usr/local/lib/python3.7/dist-packages (from konlpy) (0.4.4)
Requirement already satisfied: numpy&gt;=1.6 in /usr/local/lib/python3.7/dist-packages (from konlpy) (1.19.5)
Requirement already satisfied: tweepy&gt;=3.7.0 in /usr/local/lib/python3.7/dist-packages (from konlpy) (3.10.0)
Requirement already satisfied: lxml&gt;=4.1.0 in /usr/local/lib/python3.7/dist-packages (from konlpy) (4.2.6)
Requirement already satisfied: typing-extensions in /usr/local/lib/python3.7/dist-packages (from JPype1&gt;=0.7.0-&gt;konlpy) (3.10.0.2)
Requirement already satisfied: requests[socks]&gt;=2.11.1 in /usr/local/lib/python3.7/dist-packages (from tweepy&gt;=3.7.0-&gt;konlpy) (2.23.0)
Requirement already satisfied: requests-oauthlib&gt;=0.7.0 in /usr/local/lib/python3.7/dist-packages (from tweepy&gt;=3.7.0-&gt;konlpy) (1.3.0)
Requirement already satisfied: six&gt;=1.10.0 in /usr/local/lib/python3.7/dist-packages (from tweepy&gt;=3.7.0-&gt;konlpy) (1.15.0)
Requirement already satisfied: oauthlib&gt;=3.0.0 in /usr/local/lib/python3.7/dist-packages (from requests-oauthlib&gt;=0.7.0-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (3.1.1)
Requirement already satisfied: certifi&gt;=2017.4.17 in /usr/local/lib/python3.7/dist-packages (from requests[socks]&gt;=2.11.1-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (2021.10.8)
Requirement already satisfied: chardet&lt;4,&gt;=3.0.2 in /usr/local/lib/python3.7/dist-packages (from requests[socks]&gt;=2.11.1-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (3.0.4)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,&lt;1.26,&gt;=1.21.1 in /usr/local/lib/python3.7/dist-packages (from requests[socks]&gt;=2.11.1-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (1.24.3)
Requirement already satisfied: idna&lt;3,&gt;=2.5 in /usr/local/lib/python3.7/dist-packages (from requests[socks]&gt;=2.11.1-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (2.10)
Requirement already satisfied: PySocks!=1.5.7,&gt;=1.5.6 in /usr/local/lib/python3.7/dist-packages (from requests[socks]&gt;=2.11.1-&gt;tweepy&gt;=3.7.0-&gt;konlpy) (1.7.1)
Requirement already satisfied: nltk in /usr/local/lib/python3.7/dist-packages (3.2.5)
Requirement already satisfied: six in /usr/local/lib/python3.7/dist-packages (from nltk) (1.15.0)
</code></pre>
</div>
</div>
<section id="2-bag-of-wordsbow" class="cell markdown" id="XBKiw9Nxm51Z">
<h1>2) Bag of Words(BoW)</h1>
</section>
<div class="cell code" data-execution_count="3" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="wqQC3_Zhld-M" data-outputId="5016525a-3f27-45f6-c23a-203cd5c1170a">
<div class="sourceCode" id="cb3"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb3-1"><a href="#cb3-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> konlpy.tag <span class="im">import</span> Okt</span>
<span id="cb3-2"><a href="#cb3-2" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> re  </span>
<span id="cb3-3"><a href="#cb3-3" aria-hidden="true" tabindex="-1"></a>okt <span class="op">=</span> Okt()  </span>
<span id="cb3-4"><a href="#cb3-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-5"><a href="#cb3-5" aria-hidden="true" tabindex="-1"></a><span class="co"># 정규 표현식을 통해 온점을 제거하는 정제 작업.  </span></span>
<span id="cb3-6"><a href="#cb3-6" aria-hidden="true" tabindex="-1"></a>token <span class="op">=</span> re.sub(<span class="st">&quot;(\.)&quot;</span>,<span class="st">&quot;&quot;</span>,<span class="st">&quot;정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다.&quot;</span>)  </span>
<span id="cb3-7"><a href="#cb3-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-8"><a href="#cb3-8" aria-hidden="true" tabindex="-1"></a><span class="co"># OKT 형태소 분석기를 통해 토큰화 작업을 수행한 뒤에, token에다가 넣음.  </span></span>
<span id="cb3-9"><a href="#cb3-9" aria-hidden="true" tabindex="-1"></a>token <span class="op">=</span> okt.morphs(token)  </span>
<span id="cb3-10"><a href="#cb3-10" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-11"><a href="#cb3-11" aria-hidden="true" tabindex="-1"></a>word2index <span class="op">=</span> {}  </span>
<span id="cb3-12"><a href="#cb3-12" aria-hidden="true" tabindex="-1"></a>bow <span class="op">=</span> []  </span>
<span id="cb3-13"><a href="#cb3-13" aria-hidden="true" tabindex="-1"></a><span class="cf">for</span> voca <span class="kw">in</span> token:  </span>
<span id="cb3-14"><a href="#cb3-14" aria-hidden="true" tabindex="-1"></a><span class="co"># token을 읽으면서, word2index에 없는 (not in) 단어는 새로 추가하고, 이미 있는 단어는 넘깁니다.   </span></span>
<span id="cb3-15"><a href="#cb3-15" aria-hidden="true" tabindex="-1"></a>         <span class="cf">if</span> voca <span class="kw">not</span> <span class="kw">in</span> word2index.keys():  </span>
<span id="cb3-16"><a href="#cb3-16" aria-hidden="true" tabindex="-1"></a>             word2index[voca] <span class="op">=</span> <span class="bu">len</span>(word2index)  </span>
<span id="cb3-17"><a href="#cb3-17" aria-hidden="true" tabindex="-1"></a>             <span class="co"># BoW 전체에 전부 기본값 1을 넣는다.</span></span>
<span id="cb3-18"><a href="#cb3-18" aria-hidden="true" tabindex="-1"></a>             bow.insert(<span class="bu">len</span>(word2index)<span class="op">-</span><span class="dv">1</span>,<span class="dv">1</span>)</span>
<span id="cb3-19"><a href="#cb3-19" aria-hidden="true" tabindex="-1"></a>         <span class="cf">else</span>:</span>
<span id="cb3-20"><a href="#cb3-20" aria-hidden="true" tabindex="-1"></a>            <span class="co"># 재등장하는 단어의 인덱스</span></span>
<span id="cb3-21"><a href="#cb3-21" aria-hidden="true" tabindex="-1"></a>            index <span class="op">=</span> word2index.get(voca)</span>
<span id="cb3-22"><a href="#cb3-22" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-23"><a href="#cb3-23" aria-hidden="true" tabindex="-1"></a>            <span class="co"># 재등장한 단어는 해당하는 인덱스의 위치에 1을 더한다.</span></span>
<span id="cb3-24"><a href="#cb3-24" aria-hidden="true" tabindex="-1"></a>            bow[index] <span class="op">=</span> bow[index]<span class="op">+</span><span class="dv">1</span></span>
<span id="cb3-25"><a href="#cb3-25" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-26"><a href="#cb3-26" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(word2index)  </span></code></pre></div>
<div class="output stream stdout">
<pre><code>{&#39;정부&#39;: 0, &#39;가&#39;: 1, &#39;발표&#39;: 2, &#39;하는&#39;: 3, &#39;물가상승률&#39;: 4, &#39;과&#39;: 5, &#39;소비자&#39;: 6, &#39;느끼는&#39;: 7, &#39;은&#39;: 8, &#39;다르다&#39;: 9}
</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="4" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="oBfdGDB4lpZY" data-outputId="0301a176-f351-4d9d-9d46-b3297f088dd9">
<div class="sourceCode" id="cb5"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb5-1"><a href="#cb5-1" aria-hidden="true" tabindex="-1"></a>bow</span></code></pre></div>
<div class="output execute_result" data-execution_count="4">
<pre><code>[1, 2, 1, 1, 2, 1, 1, 1, 1, 1]</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="5" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="OlmzPtGKl9P-" data-outputId="a1e76e1b-5847-4555-e40e-195c3e7fdeb5">
<div class="sourceCode" id="cb7"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb7-1"><a href="#cb7-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> CountVectorizer</span>
<span id="cb7-2"><a href="#cb7-2" aria-hidden="true" tabindex="-1"></a>corpus <span class="op">=</span> [<span class="st">&#39;you know I want your love. because I love you.&#39;</span>]</span>
<span id="cb7-3"><a href="#cb7-3" aria-hidden="true" tabindex="-1"></a>vector <span class="op">=</span> CountVectorizer()</span>
<span id="cb7-4"><a href="#cb7-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-5"><a href="#cb7-5" aria-hidden="true" tabindex="-1"></a><span class="co"># 코퍼스로부터 각 단어의 빈도수를 기록</span></span>
<span id="cb7-6"><a href="#cb7-6" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vector.fit_transform(corpus).toarray()) </span>
<span id="cb7-7"><a href="#cb7-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-8"><a href="#cb7-8" aria-hidden="true" tabindex="-1"></a><span class="co"># 각 단어의 인덱스가 어떻게 부여되었는지를 출력</span></span>
<span id="cb7-9"><a href="#cb7-9" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vector.vocabulary_) </span></code></pre></div>
<div class="output stream stdout">
<pre><code>[[1 1 2 1 2 1]]
{&#39;you&#39;: 4, &#39;know&#39;: 1, &#39;want&#39;: 3, &#39;your&#39;: 5, &#39;love&#39;: 2, &#39;because&#39;: 0}
</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="6" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="SSxigZmzmBpE" data-outputId="f2cc3548-17b1-441b-abee-d8a01cad37fb">
<div class="sourceCode" id="cb9"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb9-1"><a href="#cb9-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> CountVectorizer</span>
<span id="cb9-2"><a href="#cb9-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb9-3"><a href="#cb9-3" aria-hidden="true" tabindex="-1"></a>text <span class="op">=</span> [<span class="st">&quot;Family is not an important thing. It&#39;s everything.&quot;</span>]</span>
<span id="cb9-4"><a href="#cb9-4" aria-hidden="true" tabindex="-1"></a>vect <span class="op">=</span> CountVectorizer(stop_words<span class="op">=</span>[<span class="st">&quot;the&quot;</span>, <span class="st">&quot;a&quot;</span>, <span class="st">&quot;an&quot;</span>, <span class="st">&quot;is&quot;</span>, <span class="st">&quot;not&quot;</span>])</span>
<span id="cb9-5"><a href="#cb9-5" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.fit_transform(text).toarray()) </span>
<span id="cb9-6"><a href="#cb9-6" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.vocabulary_)</span></code></pre></div>
<div class="output stream stdout">
<pre><code>[[1 1 1 1 1]]
{&#39;family&#39;: 1, &#39;important&#39;: 2, &#39;thing&#39;: 4, &#39;it&#39;: 3, &#39;everything&#39;: 0}
</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="7" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="oSjxoyFHmEbv" data-outputId="68e9ac13-d300-45ae-ca0c-08f8f543f7ca">
<div class="sourceCode" id="cb11"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb11-1"><a href="#cb11-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> CountVectorizer</span>
<span id="cb11-2"><a href="#cb11-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-3"><a href="#cb11-3" aria-hidden="true" tabindex="-1"></a>text <span class="op">=</span> [<span class="st">&quot;Family is not an important thing. It&#39;s everything.&quot;</span>]</span>
<span id="cb11-4"><a href="#cb11-4" aria-hidden="true" tabindex="-1"></a>vect <span class="op">=</span> CountVectorizer(stop_words<span class="op">=</span><span class="st">&quot;english&quot;</span>)</span>
<span id="cb11-5"><a href="#cb11-5" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.fit_transform(text).toarray())</span>
<span id="cb11-6"><a href="#cb11-6" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.vocabulary_)</span></code></pre></div>
<div class="output stream stdout">
<pre><code>[[1 1 1]]
{&#39;family&#39;: 0, &#39;important&#39;: 1, &#39;thing&#39;: 2}
</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="13" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="LZrIscOsmFp2" data-outputId="673cb1a5-b445-40b0-8a07-cd6c463d0846">
<div class="sourceCode" id="cb13"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb13-1"><a href="#cb13-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> CountVectorizer</span>
<span id="cb13-2"><a href="#cb13-2" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> nltk.corpus <span class="im">import</span> stopwords</span>
<span id="cb13-3"><a href="#cb13-3" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> nltk</span>
<span id="cb13-4"><a href="#cb13-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb13-5"><a href="#cb13-5" aria-hidden="true" tabindex="-1"></a>nltk.download(<span class="st">&#39;stopwords&#39;</span>)</span>
<span id="cb13-6"><a href="#cb13-6" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb13-7"><a href="#cb13-7" aria-hidden="true" tabindex="-1"></a>text <span class="op">=</span> [<span class="st">&quot;Family is not an important thing. It&#39;s everything.&quot;</span>]</span>
<span id="cb13-8"><a href="#cb13-8" aria-hidden="true" tabindex="-1"></a>sw <span class="op">=</span> stopwords.words(<span class="st">&quot;english&quot;</span>)</span>
<span id="cb13-9"><a href="#cb13-9" aria-hidden="true" tabindex="-1"></a>vect <span class="op">=</span> CountVectorizer(stop_words <span class="op">=</span>sw)</span>
<span id="cb13-10"><a href="#cb13-10" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.fit_transform(text).toarray()) </span>
<span id="cb13-11"><a href="#cb13-11" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vect.vocabulary_)</span></code></pre></div>
<div class="output stream stdout">
<pre><code>[nltk_data] Downloading package stopwords to /root/nltk_data...
[nltk_data]   Unzipping corpora/stopwords.zip.
[[1 1 1 1]]
{&#39;family&#39;: 1, &#39;important&#39;: 2, &#39;thing&#39;: 3, &#39;everything&#39;: 0}
</code></pre>
</div>
</div>
<section id="4-tf-idfterm-frequency-inverse-document-frequency" class="cell markdown" id="XzfCSHmonDvz">
<h1>4) TF-IDF(Term Frequency-Inverse Document Frequency)</h1>
</section>
<div class="cell code" data-execution_count="17" id="B4ZM5q4rnIc5">
<div class="sourceCode" id="cb15"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb15-1"><a href="#cb15-1" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> pandas <span class="im">as</span> pd <span class="co"># 데이터프레임 사용을 위해</span></span>
<span id="cb15-2"><a href="#cb15-2" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> math <span class="im">import</span> log <span class="co"># IDF 계산을 위해</span></span></code></pre></div>
</div>
<div class="cell code" data-execution_count="18" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:175}" id="baKycaGenLYn" data-outputId="f8d4f0bf-4fdb-4f88-ca61-96f14c3c3a05">
<div class="sourceCode" id="cb16"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb16-1"><a href="#cb16-1" aria-hidden="true" tabindex="-1"></a>docs <span class="op">=</span> [</span>
<span id="cb16-2"><a href="#cb16-2" aria-hidden="true" tabindex="-1"></a>  <span class="st">&#39;먹고 싶은 사과&#39;</span>,</span>
<span id="cb16-3"><a href="#cb16-3" aria-hidden="true" tabindex="-1"></a>  <span class="st">&#39;먹고 싶은 바나나&#39;</span>,</span>
<span id="cb16-4"><a href="#cb16-4" aria-hidden="true" tabindex="-1"></a>  <span class="st">&#39;길고 노란 바나나 바나나&#39;</span>,</span>
<span id="cb16-5"><a href="#cb16-5" aria-hidden="true" tabindex="-1"></a>  <span class="st">&#39;저는 과일이 좋아요&#39;</span></span>
<span id="cb16-6"><a href="#cb16-6" aria-hidden="true" tabindex="-1"></a>] </span>
<span id="cb16-7"><a href="#cb16-7" aria-hidden="true" tabindex="-1"></a>vocab <span class="op">=</span> <span class="bu">list</span>(<span class="bu">set</span>(w <span class="cf">for</span> doc <span class="kw">in</span> docs <span class="cf">for</span> w <span class="kw">in</span> doc.split()))</span>
<span id="cb16-8"><a href="#cb16-8" aria-hidden="true" tabindex="-1"></a>vocab.sort()</span>
<span id="cb16-9"><a href="#cb16-9" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-10"><a href="#cb16-10" aria-hidden="true" tabindex="-1"></a>N <span class="op">=</span> <span class="bu">len</span>(docs) <span class="co"># 총 문서의 수</span></span>
<span id="cb16-11"><a href="#cb16-11" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-12"><a href="#cb16-12" aria-hidden="true" tabindex="-1"></a><span class="kw">def</span> tf(t, d):</span>
<span id="cb16-13"><a href="#cb16-13" aria-hidden="true" tabindex="-1"></a>    <span class="cf">return</span> d.count(t)</span>
<span id="cb16-14"><a href="#cb16-14" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-15"><a href="#cb16-15" aria-hidden="true" tabindex="-1"></a><span class="kw">def</span> idf(t):</span>
<span id="cb16-16"><a href="#cb16-16" aria-hidden="true" tabindex="-1"></a>    df <span class="op">=</span> <span class="dv">0</span></span>
<span id="cb16-17"><a href="#cb16-17" aria-hidden="true" tabindex="-1"></a>    <span class="cf">for</span> doc <span class="kw">in</span> docs:</span>
<span id="cb16-18"><a href="#cb16-18" aria-hidden="true" tabindex="-1"></a>        df <span class="op">+=</span> t <span class="kw">in</span> doc</span>
<span id="cb16-19"><a href="#cb16-19" aria-hidden="true" tabindex="-1"></a>    <span class="cf">return</span> log(N<span class="op">/</span>(df <span class="op">+</span> <span class="dv">1</span>))</span>
<span id="cb16-20"><a href="#cb16-20" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-21"><a href="#cb16-21" aria-hidden="true" tabindex="-1"></a><span class="kw">def</span> tfidf(t, d):</span>
<span id="cb16-22"><a href="#cb16-22" aria-hidden="true" tabindex="-1"></a>    <span class="cf">return</span> tf(t,d)<span class="op">*</span> idf(t)</span>
<span id="cb16-23"><a href="#cb16-23" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-24"><a href="#cb16-24" aria-hidden="true" tabindex="-1"></a>result <span class="op">=</span> []</span>
<span id="cb16-25"><a href="#cb16-25" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-26"><a href="#cb16-26" aria-hidden="true" tabindex="-1"></a><span class="cf">for</span> i <span class="kw">in</span> <span class="bu">range</span>(N): <span class="co"># 각 문서에 대해서 아래 명령을 수행</span></span>
<span id="cb16-27"><a href="#cb16-27" aria-hidden="true" tabindex="-1"></a>    result.append([])</span>
<span id="cb16-28"><a href="#cb16-28" aria-hidden="true" tabindex="-1"></a>    d <span class="op">=</span> docs[i]</span>
<span id="cb16-29"><a href="#cb16-29" aria-hidden="true" tabindex="-1"></a>    <span class="cf">for</span> j <span class="kw">in</span> <span class="bu">range</span>(<span class="bu">len</span>(vocab)):</span>
<span id="cb16-30"><a href="#cb16-30" aria-hidden="true" tabindex="-1"></a>        t <span class="op">=</span> vocab[j]        </span>
<span id="cb16-31"><a href="#cb16-31" aria-hidden="true" tabindex="-1"></a>        result[<span class="op">-</span><span class="dv">1</span>].append(tf(t, d))</span>
<span id="cb16-32"><a href="#cb16-32" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-33"><a href="#cb16-33" aria-hidden="true" tabindex="-1"></a>tf_ <span class="op">=</span> pd.DataFrame(result, columns <span class="op">=</span> vocab)</span>
<span id="cb16-34"><a href="#cb16-34" aria-hidden="true" tabindex="-1"></a>tf_</span></code></pre></div>
<div class="output execute_result" data-execution_count="18">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>과일이</th>
      <th>길고</th>
      <th>노란</th>
      <th>먹고</th>
      <th>바나나</th>
      <th>사과</th>
      <th>싶은</th>
      <th>저는</th>
      <th>좋아요</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
</div>
</div>
<div class="cell code" data-execution_count="19" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:332}" id="4ncxVxw4nWtV" data-outputId="32cde61c-11e9-4883-d860-00add654faca">
<div class="sourceCode" id="cb17"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb17-1"><a href="#cb17-1" aria-hidden="true" tabindex="-1"></a>result <span class="op">=</span> []</span>
<span id="cb17-2"><a href="#cb17-2" aria-hidden="true" tabindex="-1"></a><span class="cf">for</span> j <span class="kw">in</span> <span class="bu">range</span>(<span class="bu">len</span>(vocab)):</span>
<span id="cb17-3"><a href="#cb17-3" aria-hidden="true" tabindex="-1"></a>    t <span class="op">=</span> vocab[j]</span>
<span id="cb17-4"><a href="#cb17-4" aria-hidden="true" tabindex="-1"></a>    result.append(idf(t))</span>
<span id="cb17-5"><a href="#cb17-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-6"><a href="#cb17-6" aria-hidden="true" tabindex="-1"></a>idf_ <span class="op">=</span> pd.DataFrame(result, index <span class="op">=</span> vocab, columns <span class="op">=</span> [<span class="st">&quot;IDF&quot;</span>])</span>
<span id="cb17-7"><a href="#cb17-7" aria-hidden="true" tabindex="-1"></a>idf_</span></code></pre></div>
<div class="output execute_result" data-execution_count="19">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>IDF</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>과일이</th>
      <td>0.693147</td>
    </tr>
    <tr>
      <th>길고</th>
      <td>0.693147</td>
    </tr>
    <tr>
      <th>노란</th>
      <td>0.693147</td>
    </tr>
    <tr>
      <th>먹고</th>
      <td>0.287682</td>
    </tr>
    <tr>
      <th>바나나</th>
      <td>0.287682</td>
    </tr>
    <tr>
      <th>사과</th>
      <td>0.693147</td>
    </tr>
    <tr>
      <th>싶은</th>
      <td>0.287682</td>
    </tr>
    <tr>
      <th>저는</th>
      <td>0.693147</td>
    </tr>
    <tr>
      <th>좋아요</th>
      <td>0.693147</td>
    </tr>
  </tbody>
</table>
</div>
</div>
</div>
<div class="cell code" data-execution_count="20" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:175}" id="2baP_Z29nZZX" data-outputId="081c4594-800c-439a-82ad-b87b49071335">
<div class="sourceCode" id="cb18"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb18-1"><a href="#cb18-1" aria-hidden="true" tabindex="-1"></a>result <span class="op">=</span> []</span>
<span id="cb18-2"><a href="#cb18-2" aria-hidden="true" tabindex="-1"></a><span class="cf">for</span> i <span class="kw">in</span> <span class="bu">range</span>(N):</span>
<span id="cb18-3"><a href="#cb18-3" aria-hidden="true" tabindex="-1"></a>    result.append([])</span>
<span id="cb18-4"><a href="#cb18-4" aria-hidden="true" tabindex="-1"></a>    d <span class="op">=</span> docs[i]</span>
<span id="cb18-5"><a href="#cb18-5" aria-hidden="true" tabindex="-1"></a>    <span class="cf">for</span> j <span class="kw">in</span> <span class="bu">range</span>(<span class="bu">len</span>(vocab)):</span>
<span id="cb18-6"><a href="#cb18-6" aria-hidden="true" tabindex="-1"></a>        t <span class="op">=</span> vocab[j]</span>
<span id="cb18-7"><a href="#cb18-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb18-8"><a href="#cb18-8" aria-hidden="true" tabindex="-1"></a>        result[<span class="op">-</span><span class="dv">1</span>].append(tfidf(t,d))</span>
<span id="cb18-9"><a href="#cb18-9" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb18-10"><a href="#cb18-10" aria-hidden="true" tabindex="-1"></a>tfidf_ <span class="op">=</span> pd.DataFrame(result, columns <span class="op">=</span> vocab)</span>
<span id="cb18-11"><a href="#cb18-11" aria-hidden="true" tabindex="-1"></a>tfidf_</span></code></pre></div>
<div class="output execute_result" data-execution_count="20">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>과일이</th>
      <th>길고</th>
      <th>노란</th>
      <th>먹고</th>
      <th>바나나</th>
      <th>사과</th>
      <th>싶은</th>
      <th>저는</th>
      <th>좋아요</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.287682</td>
      <td>0.000000</td>
      <td>0.693147</td>
      <td>0.287682</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.287682</td>
      <td>0.287682</td>
      <td>0.000000</td>
      <td>0.287682</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.000000</td>
      <td>0.693147</td>
      <td>0.693147</td>
      <td>0.000000</td>
      <td>0.575364</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.693147</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.693147</td>
      <td>0.693147</td>
    </tr>
  </tbody>
</table>
</div>
</div>
</div>
<div class="cell code" data-execution_count="21" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="_54T6vWxncBE" data-outputId="87df4dc8-346b-4d3e-8034-ce84e0f0f5e3">
<div class="sourceCode" id="cb19"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb19-1"><a href="#cb19-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> CountVectorizer</span>
<span id="cb19-2"><a href="#cb19-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb19-3"><a href="#cb19-3" aria-hidden="true" tabindex="-1"></a>corpus <span class="op">=</span> [</span>
<span id="cb19-4"><a href="#cb19-4" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;you know I want your love&#39;</span>,</span>
<span id="cb19-5"><a href="#cb19-5" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;I like you&#39;</span>,</span>
<span id="cb19-6"><a href="#cb19-6" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;what should I do &#39;</span>,    </span>
<span id="cb19-7"><a href="#cb19-7" aria-hidden="true" tabindex="-1"></a>]</span>
<span id="cb19-8"><a href="#cb19-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb19-9"><a href="#cb19-9" aria-hidden="true" tabindex="-1"></a>vector <span class="op">=</span> CountVectorizer()</span>
<span id="cb19-10"><a href="#cb19-10" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vector.fit_transform(corpus).toarray()) <span class="co"># 코퍼스로부터 각 단어의 빈도 수를 기록한다.</span></span>
<span id="cb19-11"><a href="#cb19-11" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(vector.vocabulary_) <span class="co"># 각 단어의 인덱스가 어떻게 부여되었는지를 보여준다.</span></span></code></pre></div>
<div class="output stream stdout">
<pre><code>[[0 1 0 1 0 1 0 1 1]
 [0 0 1 0 0 0 0 1 0]
 [1 0 0 0 1 0 1 0 0]]
{&#39;you&#39;: 7, &#39;know&#39;: 1, &#39;want&#39;: 5, &#39;your&#39;: 8, &#39;love&#39;: 3, &#39;like&#39;: 2, &#39;what&#39;: 6, &#39;should&#39;: 4, &#39;do&#39;: 0}
</code></pre>
</div>
</div>
<div class="cell code" data-execution_count="22" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="fK8Q133jne6r" data-outputId="83426fe9-09e4-4f24-b432-edd568498288">
<div class="sourceCode" id="cb21"><pre class="sourceCode python"><code class="sourceCode python"><span id="cb21-1"><a href="#cb21-1" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.feature_extraction.text <span class="im">import</span> TfidfVectorizer</span>
<span id="cb21-2"><a href="#cb21-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb21-3"><a href="#cb21-3" aria-hidden="true" tabindex="-1"></a>corpus <span class="op">=</span> [</span>
<span id="cb21-4"><a href="#cb21-4" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;you know I want your love&#39;</span>,</span>
<span id="cb21-5"><a href="#cb21-5" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;I like you&#39;</span>,</span>
<span id="cb21-6"><a href="#cb21-6" aria-hidden="true" tabindex="-1"></a>    <span class="st">&#39;what should I do &#39;</span>,    </span>
<span id="cb21-7"><a href="#cb21-7" aria-hidden="true" tabindex="-1"></a>]</span>
<span id="cb21-8"><a href="#cb21-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb21-9"><a href="#cb21-9" aria-hidden="true" tabindex="-1"></a>tfidfv <span class="op">=</span> TfidfVectorizer().fit(corpus)</span>
<span id="cb21-10"><a href="#cb21-10" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(tfidfv.transform(corpus).toarray())</span>
<span id="cb21-11"><a href="#cb21-11" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(tfidfv.vocabulary_)</span></code></pre></div>
<div class="output stream stdout">
<pre><code>[[0.         0.46735098 0.         0.46735098 0.         0.46735098
  0.         0.35543247 0.46735098]
 [0.         0.         0.79596054 0.         0.         0.
  0.         0.60534851 0.        ]
 [0.57735027 0.         0.         0.         0.57735027 0.
  0.57735027 0.         0.        ]]
{&#39;you&#39;: 7, &#39;know&#39;: 1, &#39;want&#39;: 5, &#39;your&#39;: 8, &#39;love&#39;: 3, &#39;like&#39;: 2, &#39;what&#39;: 6, &#39;should&#39;: 4, &#39;do&#39;: 0}
</code></pre>
</div>
</div>
</body>
</html>
