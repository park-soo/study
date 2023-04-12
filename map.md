## Map
### ※ Java에서 데이터를 저장하는 자료구조들을 한 곳에 모아 편리하게 관리하고 사용하기 위해 제공하는 것. 크게 List, Set, Map으로 구분할 수 있다.
- Map은 리스트나 배열처럼 순차적으로(sequential) 해당 요소 값을 구하지 않고 key를 통해 value를 얻는다.

- 맵(Map)의 가장 큰 특징이라면 key로 value를 얻어낸다는 점이다. 

-특징

1. 요소의 저장 순서를 유지하지 않습니다.

2. key :  중복을 허용  X 
   
   value :  중복은 허용 O


## Hash Map

1. HashMap<K, V> 클래스

- Map 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나입니다.
- HashMap은 Map을 구현한다. key와 value를 묶어 하나의 entry로 저장한다는 특징을 갖는다.
- 해시 알고리즘(hash algorithm)을 사용하여 많은 양의 데이터를 검색하는데 검색 속도가 매우 빠르다.
- HashMap 클래스는 Map 인터페이스를 구현하므로, 중복된 키로는 값을 저장할 수 없다.
- value에 null값도 사용 가능하다.
- 멀티쓰레드에서는 HashTable을 사용한다.( 같은 값을 다른 키로 저장하는 것은 가능 )



HashMap <k,v> 주요 메소드 <br>
- void clear() : 
- boolean containsKey(Object key)	: 
- boolean containsValue(Object value)	: 
- V get(Object key) : 
- boolean isEmpty() : 
- Set<K> keySet(): 
- Set<Map.Entry<K,V>> entrySet() : 
- V put(K key, V value) : 
- V remove(Object key) : 
- boolean remove(Object key, Object value) : 
- V replace(K key, V value) : 
- boolean replace(K key, V oldValue, V newValue) : 
- int size() :

<br><br><br><br><br>

HashMap <k,v> 주요 메소드 <br>
- void clear() : 해당 맵(map)의 모든 매핑(mapping)을 제거함.
- boolean containsKey(Object key)	: 해당 맵이 전달된 키를 포함하고 있는지를 확인함.
- boolean containsValue(Object value)	: 해당 맵이 전달된 값에 해당하는 하나 이상의 키를 포함하고 있는지를 확인함.
- V get(Object key) : 해당 맵에서 전달된 키에 대응하는 값을 반환함. 만약 해당 맵이 전달된 키를 포함한 매핑을 포함하고 있지 않으면 null을 반환함.
- boolean isEmpty() : 해당 맵이 비어있는지를 확인함.
- Set<K> keySet(): 해당 맵에 포함되어 있는 모든 키로 만들어진 Set 객체를 반환함.
- Set<Map.Entry<K,V>> entrySet() :  Map에 저장되어있는 Entry객체들을 반환한다. Entry객체는 키(Key)와 값(Value)의 쌍(Pair)을 저장하는 객체로 getKey()와 getValue() 메소드로 각각의 값을 가지고 올 수 있다.
- V put(K key, V value) : 해당 맵에 전달된 키에 대응하는 값으로 특정 값을 매핑함.
- V remove(Object key) : 해당 맵에서 전달된 키에 대응하는 매핑을 제거함.
- boolean remove(Object key, Object value) : 해당 맵에서 특정 값에 대응하는 특정 키의 매핑을 제거함.
- V replace(K key, V value) : 해당 맵에서 전달된 키에 대응하는 값을 특정 값으로 대체함.
- boolean replace(K key, V oldValue, V newValue) : 해당 맵에서 특정 값에 대응하는 전달된 키의 값을 새로운 값으로 대체함.
- int size() : 해당 맵의 매핑의 총 개수를 반환함.

```java
import java.util.HashMap;

public class TestMap {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<String, String>();
        map.put("people", "사람");
        map.put("baseball", "야구");

        System.out.println(map.get("people"));
        System.out.println(map.containsKey("people"));
        System.out.println(map.remove("people"));
        System.out.println(map.size());
    }
}

```

## Hash VS Tree VS LinkedHash

- HashMap : 내부 hash 값에 따라서 키순서가 정해지므로 특정 규칙없이 출력됨
- TreeMap : 키값이 오름차순 정렬된다. 트리에 저장되므로 키값은 일정 기준으로 정렬된 상태로 출력된다.
- LinkedHashMap : 키값은 입력 순서대로 출력되어서 나온다.

```java
Map<String, String> map = Maps.newHashMap();
map.put("c", "1");
map.put("a", "1");
map.put("b", "1");
map.put("k", "1");
for (String s : map.keySet()) {
    System.out.println(s);
}
// b, c, a, k 출력

tree ? 
linkedhash ?
```
### 결론
- 특별한 이유가 없다면 검색 성능이 좋은(O(1)) HashMap 을 사용하자
- 키값이 일정한 수준대로 iterate 하려고 한다면 TreeMap 을 사용하자. 하지만 랜덤 접근에 대해서는 O(logn) 성능을 지니므로 많은 데이터를 넣을경우 좋지 않은 성능이 나올수 있다.
- 입력 순서가 의미있다면 LinkedHashMap 을 사용하자. 랜덤 접근에 대해 O(n) 성능을 지니므로 많은 데이터를 입력할 경우 사용하지 않는것이 좋겠다.