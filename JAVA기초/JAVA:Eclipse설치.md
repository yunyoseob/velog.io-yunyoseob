안녕하세요. 😀 이번에는 JAVA: Eclipse 설치방법에 대해 포스팅하도록 하겠습니다.

## JAVA : Eclipse 설치

> **1. Eclipse 홈페이지 접속**

먼저, [Eclipse 홈페이지](https://www.eclipse.org/)로 들어갑니다.

![](https://images.velog.io/images/yunyoseob/post/902e9d94-3538-4871-aca3-f71f4137bf5f/image.png)

- Eclipse 홈페이지 화면

> **2. Eclipse 홈페이지 우측 상단에 Download를 누릅니다.**

![](https://images.velog.io/images/yunyoseob/post/3442de73-596d-4518-bb3d-ae22c1d6b75e/image.png)

> **3. Get Eclipse IDE 2021-12 아래 Download Packages를 누릅니다.**

![](https://images.velog.io/images/yunyoseob/post/8fadbdae-cd83-4898-b662-96e2afb5addc/image.png)

> **4. 우측하단에 MORE DOWNLOADS를 찾아 자신이 사용할 버전을 선택합니다.**

**✔ MORE DOWNLOADS에서 Older Versions를 누르면 버전별로 확인할 수 있습니다.**

![](https://images.velog.io/images/yunyoseob/post/afd5ccef-ce3b-4ffe-be07-6eb5c43dfe5e/image.png)

**✔ 필자는 Eclipse 2020-06(4.16)을 다운받도록 하겠습니다.**

- 필자가 현재 사용하는 java version

```java
javac -version
// javac 1.8.0_202
java -version
/*
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
*/
```

![](https://images.velog.io/images/yunyoseob/post/eff6a814-cd93-4083-bec5-6cb258720255/image.png)

> **5. Eclipse IDE for Enterprise Java Developers에서 본인의 운영체제에 맞는 것을 선택하여 줍니다.**

**✔ 필자는 Windows x86_64를 다운받도록 하겠습니다.**

![](https://images.velog.io/images/yunyoseob/post/19e580a7-460c-4c4e-ac9f-5e8446b840ce/image.png)

> **6. 추가적으로 파란상자 안에 Download안에서도 본인의 운영체제에 맞는 것을 선택하여 줍니다.**

**✔ 필자는 Windows x86_64를 선택하도록 하겠습니다.**

![](https://images.velog.io/images/yunyoseob/post/2762109d-c61b-47ab-9984-24da2bbd0f07/image.png)

> **7. Select Another Mirror를 클릭합니다.**

![](https://images.velog.io/images/yunyoseob/post/6a6b0a35-0b64-400f-a312-0c2337f7496c/image.png)

> **8. 본인이 다운받고 싶은 곳에서 클릭하여 다운받습니다.**

![](https://images.velog.io/images/yunyoseob/post/cbed605a-f1f3-4d08-a2d1-2e863c82d17e/image.png)

> **9. 다운로드가 완료되었으면, .exe 파일을 실행합니다.**

![](https://images.velog.io/images/yunyoseob/post/cc0df0e5-60e0-4572-a500-12275b2d84a9/image.png)

> **10. 파일 실행 후, 작업할 경로를 지정한 후, 설치합니다.**



## Eclipse에서 Hello Java!! 출력하기

> **11. 설치가 완료되면, Installation Folder(Work place)를 지정합니다.**


![](https://images.velog.io/images/yunyoseob/post/84d34b45-4a62-49cb-a240-d848d07361e9/image.png)

> **12. 위와 같은 화면이 나타나면 본인이 생성할 프로젝트를 설정합니다.**

![](https://images.velog.io/images/yunyoseob/post/28b70715-7b89-4689-b325-f06374e1e5ed/image.png)

![](https://images.velog.io/images/yunyoseob/post/d971a137-dbd1-40a0-8882-5962e24b8523/image.png)

![](https://images.velog.io/images/yunyoseob/post/b2c86880-7cf8-4111-b944-1b6f1f472ce8/image.png)

- Location은 본인 컴퓨터의 주소입니다. (파란색 사각형은 Masking 처리 하였습니다.)

> **13. 이제 사용할 준비가 다 되었으니, 패키지 생성후, 자유롭게 사용하면 됩니다.**

![](https://images.velog.io/images/yunyoseob/post/3413e9d3-f4bf-4a5e-83e8-f5831716384e/image.png)

✔ **Package 생성**

![](https://images.velog.io/images/yunyoseob/post/f0adbfc8-04d7-43c5-a8e9-479d39f422c5/image.png)

✔ **Class 생성**

![](https://images.velog.io/images/yunyoseob/post/a1e24cdc-907e-445c-b14c-577021aae071/image.png)

![](https://images.velog.io/images/yunyoseob/post/56ff5111-3565-4322-8035-b26d4858c93d/image.png)

> **14. Hello Java!! 출력하기**

- 소스 코드 작성

```java
package firstProject;

public class HelloJava {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		System.out.println("Hello Java!!");
	}

}
```

- 화면에서 우클릭 후 Run As => 1 Java Application 클릭

![](https://images.velog.io/images/yunyoseob/post/c8f42021-aceb-494b-9748-635a4c8c3266/image.png)

> **15. 설치부터 Hello Java!! 출력까지 끝**

![](https://images.velog.io/images/yunyoseob/post/810fd4ab-ece3-4797-9ca5-404360eca36e/image.png)

**이상으로 JAVA : Eclipse 설치 포스팅을 마치도록 하겠습니다. 😀**
