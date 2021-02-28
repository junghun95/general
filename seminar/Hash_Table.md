# Hash Table
## 🖥 Hash Table 이란
![](Hash_Table/Screen%20Shot%202021-02-28%20at%202.40.14%20PM.png)
	* 해시 테이블은 **(Key, Value)쌍으로 데이터를 저장**하는 자료구조중 하나
	* 내부적으로 **배열(Bucket)**을 사용하여 데이터를 저장하기 때문에 빠른 검색속도를 제공
	* 해시 테이블은 각각의 Key값에 **hash function**을 적용해 배열의 고유한 index를 활용해 값을 Bucket(Slot)에 저장하거나 검색
	* Hash function을 사용하는데 **추가적인 연산이 필요**
	* **Hash table의 크기가 유한**적이고 hash function의 특성상 **hash collision**이 발생할 수 밖에 없음
	* 충돌이 없거나 적으면 𝑂(1)의 상수 시간에 가까워지고, 충돌이 발생하면 할수록 성능은 점점 𝑂(n)에 가까워짐


## 🖥 Hash Function
* Hash function은 **임의의 길이를 갖는 메시지를 입력**받아 **고정된 길이의 해시값을 출력**하는 함수
* 암호 알고리즘에는 키가 사용되지만, hash function은 키를 사용하지 않으므로 같은 입력에 항상 같은 출력이 나옴
* 입력 값의 아주 일부만 변경되어도 전혀 다른 결과 값을 출력(눈사태 효과 - avalanche effect) -> 메시지의 오류나 변조를 탐지할 수 있는 무결성을 제공하기 위해 사용

## 🖥 Problems
1. 해시 충돌(Hash Collision): 해싱된 키(Hash Key)가 중복되어 해당 버킷(Bucket)에 이미 레코드가 존재하는 현상을 말함
2. 오버플로우(Overflow): 해시 충돌(Hash Collision)이 버킷(Bucket)에 할당된 슬롯(Slot) 수보다 많이 발생하면 더 이상 버킷에 값을 넣을 수 없는 현상
3. 클러스터링(Clustering): 연속된 레코드(Bucket)에 데이터가 몰리는 현상)

## 🖥 Resolve Collision
만약 위의 그림에서 **John Smith를 해시 함수를 돌려 나온 값과 Lisa Smith를 해시함수를 돌려나온 값이 동일(Collsion or confilct)** 하다면?

### 🛠 분리 연결법(Separate Chaining)
![](Hash_Table/Screen%20Shot%202021-02-28%20at%203.46.42%20PM.png)

* 한 버킷당 들어갈 수 있는 엔트리 수의 제한을 두지 않음으로써 모든 자료를 해시 테이블에 담는 것
* 해당 버킷에 데이터기 이미 있다면 **노드를 추가하여 다음 노드를 가리키는 방식(Linked List)**
* 위 그림 처럼 Linked List로 저장해 둘 경우 최근 데이터는 연결리스트의 head에 추가([이 경우  **𝑂(1)**, tail에 저장할 경우  **𝑂(𝑛)**이 됨](https://ratsgo.github.io/data%20structure&algorithm/2017/09/30/list/))
* 데이터의 주소값(Index)이 바뀌지 않음
* **부하율(Load Factor, 전체 버킷에서 사용중인 버킷의 비율)**이 100%에 가까울 수록 삽입, 삭제, 검색의 효율이 비약적으로 낮아짐(일반적으로 80%로 제한)
* 구현하기 간단하고 기본적이 자료구조로 이루어져 있음
* 테이블의 높은 부하율(Load Factor)이 예상되거나, 데이터가 크거나, 데이터의 길이가 가변일때 성능이 좋아짐
* JDK 1.8(Java 8)에서는 슬롯의 갯수가 8개 이하일 경우 연결리스트(Linked List)를 사용하며 그 이상의 경우는 트리(Tree)구조를 사용하여 검색의 효율을 높임


### 🛠 개방 주소법(Open Addressing)
* 충돌이 발생했을 경우 Linked List와 같은 추가적인 메모리를 사용하지 않고 **hash table의 빈 bucket을 이용하는 방법**
* 충돌이 발생하면 다른 버킷(Bucket)에 저장하기 때문에 데이터의 주소값(Index)이 바뀜
* 삽입시 메모리 할당 \[오버헤드] \[1]가 없으며, 메모리 할당자가 없이도 구현 가능

[1]: 오버헤드(Overhead)란 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간, 메모리등을 말함
#blowest/seminar
