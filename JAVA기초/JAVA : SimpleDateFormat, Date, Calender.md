안녕하세요. 🙂 오늘은 시간과 관련된 JAVA의 클래스의 자원 활용방법에 대해 포스팅하도록 하겠습니다.

> **System.currentTimeMillis()**

![](https://images.velog.io/images/yunyoseob/post/7faecb07-2a98-4854-8d46-33a7f0aa0ac1/image.png)

현재 시간을 milliseconds 단위까지로, 보여줍니다.

```java
public class Time_Velog {

	public static void main(String[] args) {
		long now = System.currentTimeMillis();
		System.out.println("now >>> : "+now);

	}

}
```

단, 이 때 몇년 몇월 몇일 몇시 몇분 몇초 형식으로 나오지 않습니다.

currentTimeMillis 메서드의 Returndl 다음과 같기 때문입니다.

![](https://images.velog.io/images/yunyoseob/post/8ee63b22-fa35-4e8e-baca-9022d7de4f6b/image.png)


```java
출력 결과 : now >>> : 1647074750142
```

따라서, 이를 실제 우리가 아는 년월일 시분초로 보기 위해 java.text 패키지에 있는 SimpleDateFormat 클래스를 활용합니다.

## SimpleDateFormat

System.currentTimeMillis()를 통해 구한 시간을 new SimpleDateFormat()에 인수로 yyyy, MM, dd, HH, mm, ss 형식에 맞춰 작성한 뒤, .format()을 통해 현재 시간으로 출력할 수 있습니다.

```java
import java.text.SimpleDateFormat;

public class Time_Velog {

	public static void main(String[] args) {
		long now = System.currentTimeMillis();
		System.out.println("now >>> : "+now);

		
		System.out.println("now >>> : " 
				+ new SimpleDateFormat ("yyyy년 MM월dd일 HH시mm분ss초").format(now));
		System.out.println("now >>> : " 
				+ new SimpleDateFormat ("HH시mm분ss초").format(now));	
		System.out.println("now >>> : " 
				+ new SimpleDateFormat ("ss초").format(now));	
	}

}
```
출력 결과는 다음과 같습니다.

```java
now >>> : 1647074997886
now >>> : 2022년 03월12일 17시49분57초
now >>> : 17시49분57초
now >>> : 57초
``` 

## Date 

Date 클래스는 epoch 시간을 리턴하며 1970년 1월 1일 00:00:00 시간을 기준으로 지나간 시간은 millisecond로 반환합니다.

```java
import java.util.Date;
import java.text.SimpleDateFormat;


public class Time_Velog {

	public static void main(String[] args) {
		Date d = new Date();
		System.out.println("Date d >>> : "+d);
        
		// 년 
		// public int getYear()
		int year = d.getYear();
		System.out.println("year >>> : " + year);
		year = year + 1900;
		System.out.println("year + 1900 >>> : " + year);
		
		// 월
		// public int getMonth()
		int month = d.getMonth();
		System.out.println("month >>> : " + month);	
		month = month + 1;
		System.out.println("month + 1 >>> : " + month);		
		
		// 일 
		// public int getDate()
		int date = d.getDate();
		System.out.println("date >>> : " + date);			
	}
}
```

Date 클래스에 기본생성자를 만들어서 참조변수를 통해 출력시키면 현재 시간이, "Sat Mar 12 18:11:55 KST 2022" 형식으로 출력 됩니다.

년, 월, 일로 바꾸려면 Date 클래스의 getYear(), getMonth(), getDate() 메서드를 활용하면 됩니다.

![](https://images.velog.io/images/yunyoseob/post/1c094332-d4ba-4779-90ee-f67915efcbfe/image.png)

잘 보면 Deprecated. 표시를 볼 수 있는데, 이는 사용을 지양하라는 의미로, Date 클래스의 특정 메서드들은  Calender 클래스의 get 메서드로 업데이트 되었으니 Date 클래스가 아니라, Calender 클래스에서 값을 구하라고 알려주는 것입니다.

> **출력 결과**

```java
Date d >>> : Sat Mar 12 18:11:55 KST 2022
year >>> : 122
year + 1900 >>> : 2022
month >>> : 2
month + 1 >>> : 3
date >>> : 12
```

getYear()메서드로 현재 년도를 구하면 122가 나오는데, 이유는 api에 설명이 되어있습니다.

![](https://images.velog.io/images/yunyoseob/post/9c2ca746-7735-44cc-91c4-49ab2e7a42d2/image.png)

따라서, getYear() 메서드로 년도를 구한뒤, 1900을 더해 주어야 현재 년도가 나옵니다.

getMonth()메서드의 경우, return된 value값이 0부터 11 사이이므로, 1을 더해주어야 현재 월을 구할 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/ee1c506a-845d-48f5-99a9-f527478d0cfe/image.png)

getDate() 메서드의 경우, return된 value값이 1부터 31까지이므로, 그대로 출력 하면 됩니다.

![](https://images.velog.io/images/yunyoseob/post/e54cbd04-5daa-4831-9921-5849bd6be96b/image.png)


## Calendar

java.util.TimeZone 클래스와 Calender 클래스를 통해 세계의 각 도시별 시간을 출력시킬 수도 있습니다. 활용되는 자원은 다음과 같습니다.

> **Calendar.getInstance()메서드**

![](https://images.velog.io/images/yunyoseob/post/ed072701-e3bb-46a6-a50b-01d25eb414c2/image.png)

> **TimeZone : getAvailableIDs()**

![](https://images.velog.io/images/yunyoseob/post/6562d904-2f2b-4502-9d96-f5cbddf7a425/image.png)


> **Calendar : Fields**

![](https://images.velog.io/images/yunyoseob/post/18a12e0f-cc29-4f76-b712-49ac99604c0c/image.png)

Calendar 클래스의 Fields를 보시면 YEAR, MONTH, DATE, HOUR_OF DAY, MINUTE, SECOND 등등 각각의 Filed와 설명을 볼 수 있습니다.

> **TimeZone.getTimeZone(String ID)**

String 인수를 입력하여, TimeZone 클래스의 참조변수로 할당 할 수 있습니다.  

![](https://images.velog.io/images/yunyoseob/post/0ebdcc08-9f0d-4059-9f2c-3974e9f29632/image.png)

> **코드 예시**

```java
import java.util.Calendar;
import java.util.TimeZone;


public class Time_Velog {
		public static void timeZone() {
        
			String cityID[] = TimeZone.getAvailableIDs();
			System.out.println("전세계 도시 수 >>> : " + cityID.length);
		}
		
		public static String cityTime(Calendar cd) {
			
			String time = 	"현재시간 : "
					 		+ cd.get(Calendar.YEAR) + "년 "
					 		+ (cd.get(Calendar.MONTH) + 1) + "월 "
					 		+ cd.get(Calendar.DATE) + "일 "
					 		+ cd.get(Calendar.HOUR_OF_DAY) + "시 "
					 		+ cd.get(Calendar.MINUTE) + "분 "
					 		+ cd.get(Calendar.SECOND) + "초";
			
			return time;
		}
		
		public static void main(String[] args) {
			
			// 전 세계 도시명 가져오기 
			Time_Velog.timeZone();
			
			String strID[] = {  "Asia/Seoul"
					           ,"America/New_York"
					           ,"Europe/Paris"
					           ,"Europe/London"
					           ,"Australia/Sydney"};
			String strName[] = {"서울", "뉴욕", "파리", "런던", "시드니"};
			
			// 도시시간 가져오기 
			for (int i=0; i < strID.length; i++) {
				
				TimeZone tz = TimeZone.getTimeZone(strID[i]);
				
				Calendar cd = Calendar.getInstance(tz);
				
				String t = Time_Velog.cityTime(cd);
				
				System.out.println(strName[i] + " " + t);
			}	
		}
}
```

위의 코드를 실행하면 TimeZone.getAvailableIDs()에 등록된 전세계 도시 수와 strID[]  배열에 입력한 아이디로 각 국의 시간을 구할 수 있습니다.

> **출력 결과**

```java
전세계 도시 수 >>> : 627
서울 현재시간 : 2022년 3월 12일 18시 31분 27초
뉴욕 현재시간 : 2022년 3월 12일 4시 31분 27초
파리 현재시간 : 2022년 3월 12일 10시 31분 27초
런던 현재시간 : 2022년 3월 12일 9시 31분 27초
시드니 현재시간 : 2022년 3월 12일 20시 31분 27초

```

**이상으로 JAVA : SimpleDateFormat, Date, Calender 포스팅을 마치도록 하겠습니다. 😊**
