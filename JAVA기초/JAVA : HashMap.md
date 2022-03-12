안녕하세요. 😆 오늘은 HashMap에 대해 포스팅해보도록 하겠습니다.


[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서 java.util 패키지에 가면 HashMap클래스를 볼 수 있습니다.

# HashMap

![](https://images.velog.io/images/yunyoseob/post/cfea4d05-a215-4124-89ec-bce2711c3577/image.png)

HashMap은 Key와 Value로 구성되어 있습니다. HashMap의 Key는 해당 프로그램에서 항상 유니크해야 합니다. 

HashMap의 Key와 해당 Key에 Value를 넣는 방법은 .put("Key", "Value")으로 넣을 수 있습니다. 

해당 키의 Value를 조회하는 방법은 .get("Key")로 조회할 수 있습니다. 

> **HashMap의 가장 중요한 특징은 Key가 Unique해야 하며, Key를 호출하면 Value가 나옵니다. 또한, 동일키에 새로운 Value를 넣는 경우, 마지막으로 put한 Value가 출력됩니다.**


> **코드로 살펴보는 HashMap**

```java
import java.util.ArrayList;
import java.util.HashMap;

public class HashMap_p1 {

	public static void main(String[] args) {
		HashMap hMap=new HashMap();
		
		hMap.put("사과","apple");
		hMap.put("바나나","banana");
		hMap.put("멜론","melon");
		hMap.put("복숭아","peach");
		
		System.out.println("\n 사과는 영어로 >>>> : "+hMap.get("사과"));
        
        System.out.println("\n 바나나는 영어로 >>>> : "+hMap.get("바나나"));
		System.out.println("\n 멜론은 영어로 >>>> : "+hMap.get("멜론"));
		System.out.println("\n 복숭아는 영어로 >>>> : "+hMap.get("복숭아"));
	
		hMap.put("사과","맛있다.");
		
		System.out.println("\n Value로 apple에서 맛있다 입력 후 , 사과는 >>>> : "+hMap.get("사과")+"\n");
	} 
} 
```

다음과 같은 코드가 있을 때, HashMap에 사과라는 Key에는 apple이라는 Value, 
바나나라는 Key에는 banana라는 Value, 멜론이라는 Key에는 melon이라는 Value, 복숭아라는 Key에는 peach라는 Value가 입력되었습니다.

.get("사과"), .get("바나나"), .get("멜론"), .get("복숭아") 메서드를 통해 해당 Key값에 있는 Value를 출력시킨 결과, apple, banana, melon, peach가 출력되었습니다.

그 이후, 사과라는 Key에 맛있다라는 Value를 입력하였고, .get("사과")로 해당 Key에 있는 Value를 출력 시킨 결과 마지막에 입력된 맛있다라는 Value가 출력이 된 것을 볼 수 있습니다.

```java
 사과는 영어로 >>>> : apple

 바나나는 영어로 >>>> : banana

 멜론은 영어로 >>>> : melon

 복숭아는 영어로 >>>> : peach

 Value로 apple에서 맛있다 입력 후 , 사과는 >>>> : 맛있다.
```

## HashMap vs ArrayList

HashMap과 ArrayList의 가장 큰 차이는 인덱스의 유무입니다. HashMap은 Key, Value로 이루어져, Key값을 .get()메서드로 호출하여 해당 Key에 있는 Value를 구하는 반면, ArrayList는 해당 인덱스에 있는 값을 구하여 사용합니다.

> **HashMap과 ArrayList 차이 코드 실습**

```java
import java.util.ArrayList;
import java.util.HashMap;

public class HashMap_p1 {

	public static void main(String[] args) {
		// ArrayList의 경우
		int idx=0;
	
		ArrayList aList = new ArrayList();
		for (int val=100; val<110; val++){
			aList.add(val);
		}
		System.out.println("aList >>> : "+aList+"\n");
		
		for (idx=0; idx<10; idx++){
			System.out.println("aList의  index(key) ="+idx+": value="+aList.get(idx));
		}

		// HashMap의 경우
		HashMap hMap=new HashMap();
		
		hMap.put("사과","apple");
		hMap.put("바나나","banana");
		hMap.put("멜론","melon");
		hMap.put("복숭아","peach");			
		hMap.put("사과","맛있다.");
		
		// HashMap은 index가 없다.
		
		idx=0;
		for(idx=0; idx<=3; idx++){
			System.out.println("hMap의 "+idx+"번째 값 >>> "+hMap.get(idx));
			// 전부 null로 출력된다.
		}
		
		System.out.println("\n HashMap은 Key로 찾아야한다.\n");
		
		// 출력하고 싶으면 키를 순차적으로 저장하여 출력한다.
		String[] sList={"사과","바나나","멜론","복숭아"};
		
		
		idx=0;
		String s="";
		for(idx=0; idx<=3; idx++){
			s=sList[idx];
			System.out.println("hMap의 Key : "+s+"\n hMap의 Value : "+hMap.get(s));
		}
        
	} // main method

} // HashMap_p1 class
```
> **출력 결과**

```java
aList >>> : [100, 101, 102, 103, 104, 105, 106, 107, 108, 109]

aList의  index(key) =0: value=100
aList의  index(key) =1: value=101
aList의  index(key) =2: value=102
aList의  index(key) =3: value=103
aList의  index(key) =4: value=104
aList의  index(key) =5: value=105
aList의  index(key) =6: value=106
aList의  index(key) =7: value=107
aList의  index(key) =8: value=108
aList의  index(key) =9: value=109
hMap의 0번째 값 >>> null
hMap의 1번째 값 >>> null
hMap의 2번째 값 >>> null
hMap의 3번째 값 >>> null

 HashMap은 Key로 찾아야한다.

hMap의 Key : 사과
 hMap의 Value : 맛있다.
hMap의 Key : 바나나
 hMap의 Value : banana
hMap의 Key : 멜론
 hMap의 Value : melon
hMap의 Key : 복숭아
 hMap의 Value : peach
```

먼저, ArrayList의 인덱스에는 100부터 109까지 값을 입력하였습니다. 이후 for문을 통해 각 index에 있는 값을 출력시킨 결과 100부터 109까지 정상적으로 출력되었습니다.

반면, HashMap에는 사과, 바나나, 멜론, 복숭아라는 Key값에 Value값을 입력하였고, 이를 index를 순차적으로 값을 출력시킨 결과, 전부 null값이 나오는 것을 확인 할 수 있었습니다.

> **만약, HashMap의 인덱스를 순차적으로 출력하고 싶으면, 각 Key값을 배열에 저장해놓은 뒤, 출력하면 됩니다.**

**✔ 코드**

```java
String[] sList={"사과","바나나","멜론","복숭아"};
```

**✔ 출력 결과**

```java
hMap의 Key : 사과
 hMap의 Value : 맛있다.
hMap의 Key : 바나나
 hMap의 Value : banana
hMap의 Key : 멜론
 hMap의 Value : melon
hMap의 Key : 복숭아
 hMap의 Value : peach
```

## HashMap과 ArrayList의 활용

만일, 이름이 같은 Key에 다른 Value를 입력하고 싶으면 ArrayList 배열에 HashMap을 입력하여 활용할 수 있습니다.

> **국가별 국가, 번호, 수도 Key로 각 Value 조회하는 실습 코드**

```java
import java.util.ArrayList;
import java.util.HashMap;


public class HashMap_p4 {
	public ArrayList hashMap(){
		System.out.println("2. ArrayList hasMap method 시작");
		
		HashMap hm0=new HashMap();
		System.out.println("3. 1st HashMap 생성 >>> : "+hm0);
		hm0.put("국가","한국");
		hm0.put("번호",82);
		hm0.put("수도","서울");

		HashMap hm1=new HashMap();
		System.out.println("4. 2nd HashMap 생성 >>> : "+hm1);
		hm1.put("국가","일본");
		hm1.put("번호",81);
		hm1.put("수도","도쿄");
		
		HashMap hm2=new HashMap();
		System.out.println("5. 3rd HashMap 생성 >>> : "+hm2);
		hm2.put("국가","중국");
		hm2.put("번호",86);
		hm2.put("수도","베이징");
		
		ArrayList aList=new ArrayList();
		aList.add(hm0);
		aList.add(hm1);
		aList.add(hm2);
		
		return aList;
	}
	
	public static void main(String[] args) {
		HashMap_p4 hp=new HashMap_p4();
		System.out.println("1. hp >>> : "+hp);
		
		ArrayList aList=hp.hashMap();
		System.out.println("aList.size() >>> : "+aList.size());
		
		for (int i=0; i<aList.size(); i++){
			HashMap hm=(HashMap)aList.get(i);
			
			Object obj1=hm.get("국가");
			String name1=(String)obj1;
			System.out.println("국가 >>> : "+name1);
			
			Object obj2=hm.get("번호");
			Integer num1=(Integer)obj2;
			System.out.println("번호 >>> : "+num1);
			
			Object obj3=hm.get("수도");
			String city1=(String)obj3;
			System.out.println("수도 >>> : "+city1);
			System.out.println();
		}	
	} 
} 
```

> **코드 설명**

HashMap클래스의 참조변수를 검색할 국가 수만큼 만들어 준뒤, 국가, 번호, 수도의 Key에 각 Value를 입력하여 줍니다.

그 이후, 각 HashMap의 참조변수를 ArrayList에 원소로 추가하여 줍니다.

마지막으로 배열의 인덱스의 HashMap 참조변수를 꺼내어 HashMap의 참조변수로 선언해준뒤, 키에 해당 하는 Value를 String 참조변수로 대입하여 출력합니다.

> **출력 결과**

```java
1. hp >>> : a.b.c.prac1.HashMap_p4@7852e922
2. ArrayList hasMap method 시작
3. 1st HashMap 생성 >>> : {}
4. 2nd HashMap 생성 >>> : {}
5. 3rd HashMap 생성 >>> : {}
aList.size() >>> : 3
국가 >>> : 한국
번호 >>> : 82
수도 >>> : 서울

국가 >>> : 일본
번호 >>> : 81
수도 >>> : 도쿄

국가 >>> : 중국
번호 >>> : 86
수도 >>> : 베이징
```

이렇게 ArrayList와 HashMap을 같이 활용하면 각 Key와 Value를 ArrayList 배열에 입력한 뒤, 배열에 있는 HashMap의 Key와 Value를 형변환을 통해 출력할 수 있습니다.


**이상으로 JAVA : HashMap 포스팅을 마치도록 하겠습니다. 😊**
