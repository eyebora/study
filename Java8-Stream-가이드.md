---


---

<h1 id="java8-stream-가이드">Java8 Stream 가이드</h1>
<h2 id="개요">1. 개요</h2>
<p>Java 8의 새로운 기능 Stream에 대해</p>
<h2 id="stream-api">2. Stream API</h2>
<p>Java 8의 주요 새로운 기능 중 하나는 여러가지 요소(element) 처리를 위한 매우 강력한 스트림 기능인 java.util.stream 입니다 .<br>
클래스는 Stream  이며, T 타입 기반의 Stream을 다양한 방법으로 생성할 수 있습니다.</p>
<h3 id="stream-생성">2.1. Stream 생성</h3>
<p>stream () 및 of () 메소드를 사용하여 콜렉션 또는 배열과 같은 다른 요소 소스에서 스트림을 작성</p>
<pre class=" language-java"><code class="prism  language-java">String<span class="token punctuation">[</span><span class="token punctuation">]</span> arr <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">String</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">{</span><span class="token string">"a"</span><span class="token punctuation">,</span> <span class="token string">"b"</span><span class="token punctuation">,</span> <span class="token string">"c"</span><span class="token punctuation">}</span><span class="token punctuation">;</span>
Stream<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> stream <span class="token operator">=</span> Arrays<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span>arr<span class="token punctuation">)</span><span class="token punctuation">;</span>
stream <span class="token operator">=</span> Stream<span class="token punctuation">.</span><span class="token function">of</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">,</span> <span class="token string">"b"</span><span class="token punctuation">,</span> <span class="token string">"c"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>stream 을 생성하는 쉬운 방법은 컬렉션 인터페이스를 통해 생성할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">Stream<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> stream <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="멀티쓰레딩-streams">2.2. 멀티쓰레딩 Streams</h3>
<p>tream API는 또한 스트림 요소에서 병렬 모드로 작업을 실행 하는 parallelStream () 메서드를 제공하여 멀티 스레딩을 단순화 합니다.<br>
아래 코드 는 스트림의 모든 요소에 대해 doWork () 메소드 를 병렬 로 실행할 수 있도록 합니다</p>
<pre><code class="java">
list.parallelStream().forEach(element -&gt; doWork(element));
</code></pre>
<p>h2. 3. Stream 사용법</p>
<p>스트림에서  제공하는 함수는 크게 중간 작업 (return Stream, self-return )과 연산작업 (특정 타입으로 return ) 으로 나뉩니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">long</span> count <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">distinct</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">count</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>distinct() 메서드는 이전 스트림에서 중복을 제거한 새로운 스트림을 만드는 중간 작업이고, count()는 스트림 크기를 리턴합니다.</p>
<h3 id="반복loop">3.1. 반복(loop)</h3>
<p>Stream 의 foreach는 while/for 루프 를 대체하며,  별도 index 없이 반복작업만 수행 할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">for</span> <span class="token punctuation">(</span>String string <span class="token operator">:</span> list<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>string<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>위의 for loop를  Stream으로 변경하면</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">boolean</span> isExist <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">anyMatch</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="필터링filter">3.2. 필터링(filter)</h3>
<p>filter() 메소드는 특정 조건을 만족하는 스트림의 요소를 선별할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">ArrayList<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> list <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"One"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"OneAndOnly"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"Derek"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"Change"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"factory"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"justBefore"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"Italy"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"Italy"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"Thursday"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">""</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
list<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">""</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>List  의 Stream  을 만들고 char “d” 가 포함 된 문자열만 필터링하여 새로운 Stream을 생성</p>
<pre class=" language-java"><code class="prism  language-java">Stream<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> stream <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">filter</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"d"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="변환map">3.3. 변환(map)</h3>
<p>map () 메서드를 사용하여 Stream의 요소를 새로운 요소로 변환할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> uris <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
uris<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token string">"C:\\My.txt"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Stream<span class="token operator">&lt;</span>Path<span class="token operator">&gt;</span> stream <span class="token operator">=</span> uris<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span>uri <span class="token operator">-</span><span class="token operator">&gt;</span> Paths<span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span>uri<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>위 코드는  모든 요소에 특정 람다 식을 적용하여 Stream 을 Stream<path> 로 변환하여 리턴합니다.<br>
모든 요소에 고유한 요소 시퀀스가 ​​포함 된 스트림이 있고 이러한 내부 요소의 스트림을 작성하려면 flatMap () 메소드를 사용해야합니다 .</path></p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>Detail<span class="token operator">&gt;</span> details <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
details<span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Detail</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Stream<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> stream
  <span class="token operator">=</span> details<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">flatMap</span><span class="token punctuation">(</span>detail <span class="token operator">-</span><span class="token operator">&gt;</span> detail<span class="token punctuation">.</span><span class="token function">getParts</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>이 예에서는 Detail 유형의 요소 목록이 있습니다 . 상세 클래스는 필드가 들어 부품, A는 목록 &lt;문자열&gt;. flatMap () 메소드 의 도움으로 PARTS 필드의 모든 요소 가 추출되어 새로운 결과 스트림에 추가됩니다. 그 후 초기 Stream  이 손실됩니다 .</p>
<h3 id="매칭match">3.4. 매칭(match)</h3>
<p>스트림 요소에 대해 유효성 검증을 수행할 수 있습니다. 이를 수행하려면 anyMatch(), allMatch(), noneMatch() 메소드를 사용하면 됩니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">boolean</span> isValid <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">anyMatch</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"h"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// true</span>
<span class="token keyword">boolean</span> isValidOne <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">allMatch</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"h"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// false</span>
<span class="token keyword">boolean</span> isValidTwo <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">noneMatch</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">contains</span><span class="token punctuation">(</span><span class="token string">"h"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// false</span>
</code></pre>
<h3 id="축소reduction">3.5. 축소(Reduction)</h3>
<p>Stream 요소를 순차적으로 순회하여 데이터를 누적 할 수 있도록 reduce() 메소드를 제공합니다.  첫번째(시작값), 두번째(누적값) 2개의 파라메터를 사용합니다.<br>
따라서 다음 코드를 실행할 수 있으며 결과는 26 (23 + 1 + 1 + 1)입니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> integers <span class="token operator">=</span> Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Integer reduced <span class="token operator">=</span> integers<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">reduce</span><span class="token punctuation">(</span><span class="token number">23</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>a<span class="token punctuation">,</span> b<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> a <span class="token operator">+</span> b<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="수집collect">3.6. 수집(collect)</h3>
<p>collect() 모든 요소를 특정 타입으로 수집??(축소)하여 리턴합니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> resultList 
  <span class="token operator">=</span> list<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">map</span><span class="token punctuation">(</span>element <span class="token operator">-</span><span class="token operator">&gt;</span> element<span class="token punctuation">.</span><span class="token function">toUpperCase</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span>Collectors<span class="token punctuation">.</span><span class="token function">toList</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>위 코드는 collect () 작업을 사용하여 Stream 을 List으로 변환합니다.</p>
<p>h2. 4. 결론</p>
<p>여기에서는 Java 스트림에 대해 간략히 살펴 보았습니다. JPA 결합하여 사용하면 복잡한 쿼리를 단순하게 하여 코드로 처리할 수 있습니다.</p>
<blockquote>
<p>작성자 : <a href="https://github.com/eyebora">eyebora32</a><br>
참조 : <a href="https://www.baeldung.com/java-8-streams">https://www.baeldung.com/java-8-streams</a><br>
Written with <a href="https://stackedit.io/">StackEdit</a></p>
</blockquote>

