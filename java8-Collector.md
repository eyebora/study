---


---

<h1 id="java8-collectors-가이드">Java8 Collectors 가이드</h1>
<h2 id="개요">1. 개요</h2>
<p>스트림의 마지막 단계에서 사용되는 Collectors에 대해 설명합니다.</p>
<h2 id="stream.collect--method">2. Stream.collect()  Method</h2>
<p>Stream.collect () 는 Java 8의 Stream API에서 제공하는  메소드입니다 . Stream 인스턴스에 보관 된 데이터 요소에 대해 변경 가능한 Grouping 작업 (요소를 일부 데이터 구조로 재 포장 및 추가 논리 적용, 연결 등)을 수행 할 수 있습니다.<br>
이러한 작업 Grouping 작업은  Collector 인터페이스를 통해 제공됩니다 .</p>
<h2 id="collectors">3. Collectors</h2>
<p>모든 구현은 Collectors 클래스 에서 찾을 수 있으며, 가독성을 높이기 위해 다음 static import를 사용하는 것이 일반적입니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">import</span> <span class="token keyword">static</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>stream<span class="token punctuation">.</span>Collectors<span class="token punctuation">.</span>*<span class="token punctuation">;</span>
</code></pre>
<p>아니면 개별적으로 선언할수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">import</span> <span class="token keyword">static</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>stream<span class="token punctuation">.</span>Collectors<span class="token punctuation">.</span>toList<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token keyword">static</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>stream<span class="token punctuation">.</span>Collectors<span class="token punctuation">.</span>toMap<span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token keyword">static</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>stream<span class="token punctuation">.</span>Collectors<span class="token punctuation">.</span>toSet<span class="token punctuation">;</span>
</code></pre>
<p>여기서는  아래의 리스트를 가지고 설명합니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> givenList <span class="token operator">=</span> Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">,</span><span class="token string">"bb"</span><span class="token punctuation">,</span><span class="token string">"ccc"</span><span class="token punctuation">,</span><span class="token string">"dd"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.tolist">3.1.  Collectors.toList()</h3>
<p>toList() 메소드는  Stream의 모든 요소를 List 인스턴스로 변환하는 데 사용할 수 있습니다 . 이 메소드를 사용하여 특정 List 구현을 없습니다. 다른 형태의 컬렉션으로 반환하려면  toCollection() 메소드를 사용해야 합니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">toList</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.toset">3.2.  Collectors.toSet()</h3>
<p>toSet() 메소드는 Stream의 모든 요소를 Set 인스턴스로 변환하는 데 사용할 수 있습니다 .</p>
<pre class=" language-java"><code class="prism  language-java">Set<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> set <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">toSet</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Set는 중복 요소를 허요하지 않으며, 컬렉션에 서로 같은 요소가 포함 된 경우 결과  Collection에 한개만 생성됩니다.</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> listWithDuplicates 
 <span class="token operator">=</span> Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">,</span> <span class="token string">"bb"</span><span class="token punctuation">,</span> <span class="token string">"c"</span><span class="token punctuation">,</span> <span class="token string">"d"</span><span class="token punctuation">,</span> <span class="token string">"bb"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Set<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> result 
 <span class="token operator">=</span> listWithDuplicates<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">toSet</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">hasSize</span><span class="token punctuation">(</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.tocollection">3.3.  Collectors.toCollection()</h3>
<p>toSet 및 toList 는 해당 Collection을 지정할수 없습니다. 사용자 정의한 Collection을 사용하려면 toCollection 메소드를 사용해야합니다 .</p>
<p>LinkedList로 Stream을 변환하는 예제:</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> result 
<span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">toCollection</span><span class="token punctuation">(</span>LinkedList<span class="token operator">:</span><span class="token operator">:</span><span class="token keyword">new</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>변경이 불가능한 Collection에서는 사용이 불가능하며, 이런 경우 collectingAndThen() 메소드를 사용하여 사용자정의 Collector를 사용해야 합니다.</p>
<h3 id="collectors.tomap">3.4.  Collectors.toMap()</h3>
<p>toMap Collector는 Stream의 요소를 Map으로 변환하는데 사용합니다. 변환하기 위해서는 keyMapper와 valueMapper 함수를 제공해야합니다.</p>
<ul>
<li>keyMapper</li>
<li>valueMapper</li>
</ul>
<p>keyMapper 는 Stream의 요소를 추출하는 key로써 사용되고, valueMapper 는 주어진 key Stream의 요소를 반환하는데 사용합니다.</p>
<p>문자열을 key로 지정하고 문자열의 길이를 value로 저장하는 Map으로 반환하는 Collector 예시:</p>
<pre class=" language-java"><code class="prism  language-java">Map<span class="token operator">&lt;</span>String<span class="token punctuation">,</span> Integer<span class="token operator">&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">toMap</span><span class="token punctuation">(</span>Function<span class="token punctuation">.</span><span class="token function">identity</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> String<span class="token operator">:</span><span class="token operator">:</span>length<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.collectingandthen">3.5.  Collectors.collectingAndThen()</h3>
<p>collectingAndThen() 은 수집 이 끝난 직후 결과에 대해 다른 작업을 수행 할 수 있는 Collector입니다.<br>
Stream 요소를 List 인스턴스 로 수집 한 다음 결과를 ImmutableList 로 변환합니다 .</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">collectingAndThen</span><span class="token punctuation">(</span><span class="token function">toList</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> ImmutableList<span class="token operator">:</span><span class="token operator">:</span>copyOf<span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="collectors.joining">3.6.  Collectors.joining()</h3>
<p>Stream  요소 를 결합하는 데 join()을 사용할 수 있습니다 .<br>
다음을 수행하여 함께 참여할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">String result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">joining</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>결과는 다음과 같습니다.</p>
<pre><code>"abbcccdd"
</code></pre>
<p>사용자 정의 구분 기호 지정할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">String result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">joining</span><span class="token punctuation">(</span><span class="token string">" "</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>결과는 다음과 같습니다.</p>
<pre><code>"a bb ccc dd"
</code></pre>
<p>접두사 , 접미사를 지정할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">String result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">joining</span><span class="token punctuation">(</span><span class="token string">" "</span><span class="token punctuation">,</span> <span class="token string">"PRE-"</span><span class="token punctuation">,</span> <span class="token string">"-POST"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>결과는 다음과 같습니다.</p>
<pre><code>"PRE-a bb ccc dd-POST"
</code></pre>
<h3 id="collectors.counting">3.7.  Collectors.counting()</h3>
<p>counting() 은 모든 Stream 요소를 간단히 카운팅 할 수 있습니다 .</p>
<pre class=" language-java"><code class="prism  language-java">String result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">joining</span><span class="token punctuation">(</span><span class="token string">" "</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.summarizingdoublelongint">3.8.  Collectors.summarizingDouble/Long/Int()</h3>
<p>summarizingDouble / Long / Int  메소드 는 Stream  요소에서 숫자 데이터에 대한 통계 정보를 제공합니다.<br>
다음을 수행하여 문자열 길이에 대한 정보를 얻을 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">DoubleSummaryStatistics result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">summarizingDouble</span><span class="token punctuation">(</span>String<span class="token operator">:</span><span class="token operator">:</span>length<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>이 경우 다음이 적용됩니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">.</span><span class="token function">getAverage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">.</span><span class="token function">getCount</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">.</span><span class="token function">getMax</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">.</span><span class="token function">getMin</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">.</span><span class="token function">getSum</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">isEqualTo</span><span class="token punctuation">(</span><span class="token number">8</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.averagingdoublelongint">3.9.  Collectors.averagingDouble/Long/Int()</h3>
<p>averagingDouble / Long / Int 는 추출 된 요소의 평균을 반환합니다.</p>
<p>다음을 수행하여 평균 문자열 길이를 얻을 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">Double result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">averagingDouble</span><span class="token punctuation">(</span>String<span class="token operator">:</span><span class="token operator">:</span>length<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.summingdoublelongint">3.10.  Collectors.summingDouble/Long/Int()</h3>
<p>summingDouble / Long / Int 는 추출 된 요소의 합계를 반환합니다.<br>
다음을 수행하여 모든 문자열 길이의 합계를 얻을 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">Double result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">summingDouble</span><span class="token punctuation">(</span>String<span class="token operator">:</span><span class="token operator">:</span>length<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="collectors.maxbyminby">3.11.  Collectors.maxBy()/minBy()</h3>
<p>maxBy / MinBy 수집기 는 제공된 스트림 의 가장 큰 / 가장 작은 요소를 반환합니다 .<br>
다음을 수행하여 가장 큰 요소를 선택할 수 있습니다.</p>
<pre class=" language-java"><code class="prism  language-java">Optional<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">maxBy</span><span class="token punctuation">(</span>Comparator<span class="token punctuation">.</span><span class="token function">naturalOrder</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>반환 된 값은 Optional 인스턴스에 래핑됩니다 . 이로 인해 사용자는 Optional이 비어있는 케이스를 고려해야 합니다.</p>
<h3 id="collectors.groupingby">3.12.  Collectors.groupingBy()</h3>
<p>groupingBy 메소드는 주어진 조건에 따라 오브젝트를 그룹화하고 결과를 Map 인스턴스 에 저장하는 데 사용됩니다 .<br>
문자열 길이로 그룹화하고 그룹화 결과를 Set 인스턴스 에 저장하는 예제:</p>
<pre class=" language-java"><code class="prism  language-java">Map<span class="token operator">&lt;</span>Integer<span class="token punctuation">,</span> Set<span class="token operator">&lt;</span>String<span class="token operator">&gt;&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">groupingBy</span><span class="token punctuation">(</span>String<span class="token operator">:</span><span class="token operator">:</span>length<span class="token punctuation">,</span> <span class="token function">toSet</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>처리결과</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token function">assertThat</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">containsEntry</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token function">newHashSet</span><span class="token punctuation">(</span><span class="token string">"a"</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">containsEntry</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token function">newHashSet</span><span class="token punctuation">(</span><span class="token string">"bb"</span><span class="token punctuation">,</span> <span class="token string">"dd"</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">containsEntry</span><span class="token punctuation">(</span><span class="token number">3</span><span class="token punctuation">,</span> <span class="token function">newHashSet</span><span class="token punctuation">(</span><span class="token string">"ccc"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>groupingBy 메소드 의 두 번째 인수 는 Collector 이며 원하는 Collector 를 자유롭게 사용</p>
<h3 id="collectors.partitioningby">3.13.  Collectors.partitioningBy()</h3>
<p>PartitioningBy 는 스트림 요소를 부울 값을 키로, 컬렉션을 값으로 저장 하는 Map 으로 반환 하는 groupingBy 의 특수한 경우입니다 .</p>
<pre class=" language-java"><code class="prism  language-java">Map<span class="token operator">&lt;</span>Boolean<span class="token punctuation">,</span> List<span class="token operator">&lt;</span>String<span class="token operator">&gt;&gt;</span> result <span class="token operator">=</span> givenList<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
  <span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">partitioningBy</span><span class="token punctuation">(</span>s <span class="token operator">-</span><span class="token operator">&gt;</span> s<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">&gt;</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<p>처리 결과는 다음과 같습니다.</p>
<pre><code>{false=["a", "bb", "dd"], true=["ccc"]}
</code></pre>
<h3 id="collectors.teeing">3.14.  Collectors.teeing()</h3>
<p>지금까지 배운 콜렉터를 사용하여 주어진 스트림 에서 최대 및 최소 수를 찾으십시오 .</p>
<pre class=" language-java"><code class="prism  language-java">List<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> numbers <span class="token operator">=</span> Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token number">42</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">24</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Optional<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> min <span class="token operator">=</span> numbers<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">minBy</span><span class="token punctuation">(</span>Integer<span class="token operator">:</span><span class="token operator">:</span>compareTo<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
Optional<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> max <span class="token operator">=</span> numbers<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">maxBy</span><span class="token punctuation">(</span>Integer<span class="token operator">:</span><span class="token operator">:</span>compareTo<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">// do something useful with min and max</span>
</code></pre>
<p>서로 다른 두 수집기를 사용하고 그 결과를 결합하여 만듭니다. Java 12 이전에는 이러한 사용 사례를 다루기 위해 주어진 스트림에서 두 번 작업하고 중간 결과를 임시 변수에 저장 한 다음 그 결과를 결합해야했습니다.<br>
다행히도 Java 12는 이러한 단계를 대신하여 내장 콜렉터를 제공합니다. 두 콜렉터와 결합기 기능을 제공하기 만하면됩니다.</p>
<pre class=" language-java"><code class="prism  language-java">numbers<span class="token punctuation">.</span><span class="token function">stream</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">collect</span><span class="token punctuation">(</span><span class="token function">teeing</span><span class="token punctuation">(</span>
  <span class="token function">minBy</span><span class="token punctuation">(</span>Integer<span class="token operator">:</span><span class="token operator">:</span>compareTo<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">// The first collector</span>
  <span class="token function">maxBy</span><span class="token punctuation">(</span>Integer<span class="token operator">:</span><span class="token operator">:</span>compareTo<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">// The second collector</span>
  <span class="token punctuation">(</span>min<span class="token punctuation">,</span> max<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token comment">// Receives the result from those collectors and combines them</span>
<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="마무리">4. 마무리</h2>
<p>이제 JPA에서 Stream과 Collector를 심층적으로 사용할 수 있습니다.</p>
<blockquote>
<p>작성자 : <a href="https://github.com/eyebora">eyebora32</a><br>
참조 : <a href="https://www.baeldung.com/java-8-collectors">https://www.baeldung.com/java-8-collectors</a><br>
Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

