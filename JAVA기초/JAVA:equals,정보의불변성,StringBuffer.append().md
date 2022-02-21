안녕하세요. 😊 오늘은 JAVA : equals, 정보의 불변성, StringBuffer.append()에 대해 알아보도록 하겠습니다.

## equals

equals는 두 값이 동일한지를 비교할 때 사용하는 메서드입니다.

[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서

java.lang의 기초자료형과 String의 equals의 메서드를 찾아보면 다음과 같은 결과를 볼 수 있습니다.

> **Java™ Platform Standard Ed. 8 equals**

|Class|Modifier and Type|Description|Detail|
|------|---|---|---|
|Boo  lean|boolean|public boolean equals(Object obj)|a Boolean object that represents **the same boolean value** as this object.|
|Byte|boolean|public boolean equals(Object obj)|Byte object that contains **the same byte value** as this object.|
|Short|boolean|public boolean equals(Object obj)|a Short object that contains **the same short value** as this object.|
|Chara cter|boolean|public boolean equals(Object obj)|a Character object that represents **the same char value** as this object.|
|Integer|boolean|public boolean equals(Object obj)|an Integer object that contains **the same int value** as this object.|
|Long|boolean|public boolean equals(Object obj)|a Long object that contains **the same long value** as this object.|
|Float|boolean|public boolean equals(Object obj)| Float object that represents **a float with the same value as the float represented by this object.**|
|Double|boolean|public boolean equals(Object obj)| a Double object that represents a double that has **the same value as the double represented by this object.**|
|Stinrg|boolean|public boolean equals(Object anObject)|a String object that represents **the same sequence of characters** as this object.|

> **Object.equals(Object)**

|Class|Modifier and Type|Method|Description|
|------|---|---|---|
|Object|boolean|equals(Object obj)|public boolean equals(Object obj)|

✔ Object.equals(Object)의 경우 Detail 설명의 경우, 다른 변수와는 조금 다릅니다.

![](https://images.velog.io/images/yunyoseob/post/7fef7850-600f-4cbc-9f4e-eca9a0ffaa14/image.png)

### equals 실습

해당 실습에서는 연산자 중 하나인 **상등 연산자 (==)**와 **equals** 차이, 그리고 Object에서의 equals와 타 변수의 equals를 비교하는 실습을 진행하도록 하겠습니다.

> **Object equals vs String equals**

```java
package a.b.c.prac1;

public class Exam_EqualsTest {
	public void objTest(Object obj_1, Object obj_2){
		boolean bool_obj;
		System.out.println("\n 3. obj_1 참조변수 주소값(o) >>> : "+obj_1);
		System.out.println("\n 4. obj_2 참조변수 주소값(o1) >>> : "+obj_2);
		System.out.println("\n 5. obj_1의 identityHashcode(진수의 차이일뿐) >>> : "+System.identityHashCode(obj_1));
		System.out.println("\n 6. obj_2의 identityHashcode(진수의 차이일뿐) >>> : "+System.identityHashCode(obj_2));
		
		bool_obj=obj_1.equals(obj_2);
		System.out.println("\n 7. objTest 결과  >>> : "+bool_obj);
	}
	
	public void strTest(String str_1, String str_2){
		boolean bool_str;
		System.out.println("\n 8. str_1 >>> : "+System.identityHashCode(str_1));
		System.out.println("\n 9. str_2 >>> : "+System.identityHashCode(str_2));
		bool_str=str_1.equals(str_2);
		System.out.println("\n 10. strTest 결과 >>> : "+bool_str);
	}
	
	
	public static void main(String[] args) {
		System.out.println("1. main method 시작 ");
		Object o=new Object();
		Object o1=new Object();
		String s="abc";
		String s1="abc";

		Exam_EqualsTest et=new Exam_EqualsTest();
		System.out.println("2. Exam_EqualsTest et >>> : "+et);
		et.objTest(o, o1);
		et.strTest(s, s1);
	}

}
```

✔ 출력 결과

```javascript
1. main method 시작 
2. Exam_EqualsTest et >>> : a.b.c.prac1.Exam_EqualsTest@15db9742

3. obj_1 참조변수 주소값(o) >>> : java.lang.Object@6d06d69c

4. obj_2 참조변수 주소값(o1) >>> : java.lang.Object@7852e922

5. obj_1의 identityHashcode(진수의 차이일뿐) >>> : 1829164700

6. obj_2의 identityHashcode(진수의 차이일뿐) >>> : 2018699554

7. objTest 결과  >>> : false

8. str_1 >>> : 1311053135

9. str_2 >>> : 1311053135

10. strTest 결과 >>> : true
```

출력 결과에서 볼 수 있듯이, Object 참조변수 obj_1와 obj_2를 비교할 시에는, 

서로 System.identityHashCode가 다르고, 참조변수 주소값이 다른 것을 볼 수 있습니다. (5,6번과 3,4번은 진수의 차이입니다.) 그 결과 **obj_1.equals(obj_2) => false**가 나온 것을 확인 할 수 있습니다.

한 편, String 변수는 System.identityHashCode가 동일한 것을 확인 할 수 있습니다. 그 결과 **str_1.equals(str_2) => true**가 나온 것을 확인 할 수 있습니다.

> **==(상등 연산자) vs equals**

```java
package a.b.c.ch4;

public class Exam_EqualsTest_1 {

	public static void main(String[] args) {
		
		String s = new String("abc");
		String s1 = new String("abc");		
		System.out.println("s >>> : " + s);
		System.out.println("s1 >>> : " + s1);
		System.out.println("System.identityHashCode(s) s >>> : " + System.identityHashCode(s));
		System.out.println("System.identityHashCode(s1) s1 >>> : " + System.identityHashCode(s1));
		
		System.out.println("s == s1 ::: " + (s == s1));
		System.out.println("s.equals(s1) ::: " + s.equals(s1));
		
		Integer i = new Integer(100);
		Integer i1 = new Integer(100);			
		System.out.println("i >>> : " + i);
		System.out.println("i1 >>> : " + i1);
		System.out.println("System.identityHashCode(s) i >>> : " + System.identityHashCode(i));
		System.out.println("System.identityHashCode(s1) i1 >>> : " + System.identityHashCode(i1));		
				
		System.out.println("(i == i1) ::: " + (i == i1));
		System.out.println("i.equals(i1) ::: " + i.equals(i1));		
	}
}
```
✔ 출력 결과

```javascript
s >>> : abc
s1 >>> : abc
System.identityHashCode(s) s >>> : 366712642
System.identityHashCode(s1) s1 >>> : 1829164700
s == s1 ::: false
s.equals(s1) ::: true
i >>> : 100
i1 >>> : 100
System.identityHashCode(s) i >>> : 2018699554
System.identityHashCode(s1) i1 >>> : 1311053135
(i == i1) ::: false
i.equals(i1) ::: true
```

new 인스턴스 연산자를 통해 String, Integer 클래스에 참조변수를 생성하는 경우, 해당 identityHashCode가 서로 다른 것을 확인 할 수 있습니다.

이 때, ==(상등 연산자)로 비교하게 되면, false가 나옵니다. 그러나 equals로 비교하게 된다면, 문자열이 s와 s1 둘 다 "abc"이기 때문에, true가 나옵니다.

마찬가지로, Integer 클래스도 ==(상등 연산자)로 비교하게 되면, false가 나옵니다. 그러나 equals로 비교하게 되면, 둘 다 100이기 때문에, true가 나옵니다.

equals로 비교하게 될 시, true가 나오는 이유는 위의 **Java™ Platform Standard Ed. 8 equals** 표를 보시면 이해가 쉽습니다. 🙂

> **JAVA에서 경우에 따라 ==(상등 연산자)와 equals의 결과가 다르게 나오기 때문에, 조심해서 사용해야합니다.**

## 정보의 불변성

JAVA에서 String 변수와 String 변수를 합치는 방법으로 concat이 있습니다.

|Modifier and Type|Method|Description|Detail|
|---|---|---|---|
|String|concat(String str)|public String concat(String str)|a String object is returned that represents a character sequence that is the concatenation of the character sequence represented by this String object and the character sequence represented by the argument string.|

> **JAVA에서 String 변수와 String 변수를 합치는 concat 코드 예시**

```java
package a.b.c.prac1;

public class String_p {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		String s0=new String("VELOG");
		String s1=new String("_POSTING");
		
		System.out.println("s0 >>> : "+s0);
		System.out.println("s1 >>> : "+s1);
		System.out.println("System.identityHashCode(s0) >>> : "+System.identityHashCode(s0));
		System.out.println("System.identityHashCode(s1) >>> : "+System.identityHashCode(s1));
		
        //=====================
		String s2=s0.concat(s1);
        //=======================
		System.out.println("s2 >>> : "+s2);
		System.out.println("System.identityHashCode(s2) >>> : "+System.identityHashCode(s2));		
	

	String sb0=new String("VELOG_POSTING");
	System.out.println("sb0 >>> : "+sb0);
	System.out.println("System.identityHaschCode(sb0) sb0 >>> : "+System.identityHashCode(sb0));
	} 
}
```

**✔ 출력 결과**

```javascript
s0 >>> : VELOG
s1 >>> : _POSTING
System.identityHashCode(s0) >>> : 366712642
System.identityHashCode(s1) >>> : 1829164700
s2 >>> : VELOG_POSTING
System.identityHashCode(s2) >>> : 2018699554
sb0 >>> : VELOG_POSTING
System.identityHaschCode(sb0) sb0 >>> : 1311053135
```

String s0과 String s1 변수를 concat 메서드를 통해 더한 결과 VELOG와 _POSTING이 합쳐져, VELOG_POSTING이 된 것을 확인 할 수 있습니다.

> **🤔 HashCode가 왜 전부 다르죠??**

String s0과 s1이 합쳐지면 한 주소에 합친 String 문자열이 나타나지 않고, 또 다른 주소(HashCode)가 생성되는 것을 확인 할 수 있습니다. 또한, 같은 내용인 VELOG_POSTING을 new 키워드로 인스턴스해도 또 다른 주소가 생성되는 것을 볼 수 있습니다.

이렇게 두 개의 String을 concat으로 합칠 경우, 새로운 주소에 저장되어, 각각의 객체의 주소를 변하지 않게 하는 것을 **정보의 불변성이라고 합니다.**

##  StringBuffer.append()

그런데, 데이터를 새로 추가하여 붙일 때 마다, VELOG 주소 하나, POSING 주소 하나, 이 둘을 concat한 VELOG_POSTING 주소하나, 이렇게 각각의 주소가 생성되면, 데이터를 추가함에 있어서 비효율적일 것입니다.

정보의 불변성은 해당 객체 주소를 유지할 수 있다는 장점은 있지만, 새로운 정보를 지속적으로 추가하여 합쳐야 할 경우, 같은 주소에 추가하지 못하고, 계속 다른 주소를 만들어내는 단점 또한 존재합니다.

이러한 정보의 불변성을 보완한 방법이 StringBuffer 클래스의 append 메서드 입니다.

> **StringBuffer.append() 코드 실습**

```java

package a.b.c.prac1;

public class StringBuffer_p {
	
	public static String getBoaradSelectAllQuery() {
	StringBuffer sb=new StringBuffer();
	System.out.println("\n start sb >>> : "+sb.hashCode());
	
	sb.append(" SELECT 								\n");
	sb.append("      A.BNUM 		BNUM 			\n");
	sb.append("		,A.BSUBJECT  	BSUBJECT 		\n");
	sb.append("		,A.BWRITER  	BWRITER 		\n");
    sb.append("		,A.BPW  		BPW   			\n");	    	    	    
    sb.append("		,A.BMEMO  		BMEMO			\n");
    sb.append("		,A.BPHOTO  		BPHOTO			\n");	 
    sb.append("		,A.DELETEYN  	DELETEYN		\n");	
    sb.append("		,TO_CHAR(A.INSERTDATE, 'YYYY-MM-DD')  INSERTDATE	\n");
    sb.append("		,TO_CHAR(A.UPDATEDATE, 'YYYY-MM-DD')  UPDATEDATE	\n");	   
    sb.append("	FROM 								\n");
    sb.append("		 MVC_BOARD A 					\n");
    sb.append("	WHERE A.DELETEYN = 'Y'				\n");
    sb.append("	ORDER BY 1 DESC  					\n");
    
    System.out.println("\n end sb >>> : "+sb.hashCode());
    return sb.toString();	
}	

	public static void main(String[] args) {
		String sqlQuery=StringBuffer_p.getBoaradSelectAllQuery();
		System.out.println("sqlQuery \n "+sqlQuery);
	}
}
```

> **출력 결과**

```javascript
start sb >>> : 366712642

end sb >>> : 366712642
sqlQuery 
  SELECT 								
      A.BNUM 		BNUM 			
		,A.BSUBJECT  	BSUBJECT 		
		,A.BWRITER  	BWRITER 		
		,A.BPW  		BPW   			
		,A.BMEMO  		BMEMO			
		,A.BPHOTO  		BPHOTO			
		,A.DELETEYN  	DELETEYN		
		,TO_CHAR(A.INSERTDATE, 'YYYY-MM-DD')  INSERTDATE	
		,TO_CHAR(A.UPDATEDATE, 'YYYY-MM-DD')  UPDATEDATE	
	FROM 								
		 MVC_BOARD A 					
	WHERE A.DELETEYN = 'Y'				
	ORDER BY 1 DESC  
```

생성자를 만들어서, String sqlQuery로 저장하고, 출력시켰을 때, 결과입니다.

**✔ 처음, sb 참조변수가 getBoaradSelectAllQuery 메서드에서 생성되고 .append를 통해 정보가 추가된 뒤에 마지막에 sb 참조변수를 다시 hashCode로 변환하여 확인해보면, 주소가 같은 것을 확인 할 수 있습니다.**

**✔ getBoaradSelectAllQuery 메서드에서 return값에 toString()을 사용하는 이유는 String 클래스와 StringBuffer 클래스는 다르기 때문에, 형변환을 사용해주어야 하기 때문입니다.**

이상으로 **JAVA : equals, 정보의 불변성, StringBuffer.append()** 포스팅을 마치도록 하겠습니다. 🙂
