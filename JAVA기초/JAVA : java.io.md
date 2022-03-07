안녕하세요 😀 오늘은 java.io에 대해 알아보도록 하겠습니다.

[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서
java.io를 클릭하여 Classes를 살펴보면, FileInputStream, FileOutputStream, File, FileReader, FileWriter, BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter 등등 많은 클래스가 존재합니다.

## File

> **Constructor**

![](https://images.velog.io/images/yunyoseob/post/731298de-ea4b-4a88-9444-3b68fdec3d7b/image.png)

java.io.File의 constructers를 보시면, File(String pathname)이 있습니다. 

이는 파일의 절대 경로를 입력하여 생성자를 생성하는 것을 의미합니다.

```java
File f=new File(파일의절대경로)
```

java.io.File에 절대 경로를 입력하였으면, 파일이 존재하는지 확인해보아야 겠지요? 🤔

> **method**

![](https://images.velog.io/images/yunyoseob/post/9f6dde94-eb3a-4e89-a131-23267c0944a8/image.png)

```java
f.exists()
```

java.io.File의 methods 중에 exists() 함수를 통해 파일 혹은 디렉토리의 존재 여부를 확인합니다. 

## FileInputStream

> **Constructor**

![](https://images.velog.io/images/yunyoseob/post/d2016b0f-f891-40e7-827a-b42999e5d33b/image.png)

java.io.FileInputStream의 constructers를 보시면, FileInputStream(File file)이 있습니다. 

이는 File 클래스의 참조변수 file을 입력하여 생성자를 생성하는 것을 의미합니다.

```java
FileInputStream fis=new FileInputStream(파일)
```
> **method**

![](https://images.velog.io/images/yunyoseob/post/2d58edb2-79bf-4164-bc54-84c83fcf3dcf/image.png)

java.io.FileInputStream의 methods 중에 read() 함수를 통해 파일 혹은 디렉토리의 존재 여부를 확인합니다. 

```java
int data=0;
data=fis.read()
```

## FileOutputStream

> **Constructor**

![](https://images.velog.io/images/yunyoseob/post/909b12a5-7ee4-481c-9e1b-49736fb2e236/image.png)

java.io.FileOutputStream의 constructers를 보시면, 
FileOutputStream(String name, boolean append)이 있습니다. 

```java
FileOutputStream fos=new File(outFile, true);
// String outFile=파일의 절대경로
```

> **method**

![](https://images.velog.io/images/yunyoseob/post/c95d2fdb-adfa-405e-9a9a-010b69690871/image.png)

java.io.FileOutputStream의 methods 중에 write(int b) 함수를 통해 파일의 특정 byte를 작성할 수 있습니다.

## BufferedInputStream

> **Constructor**

![](https://images.velog.io/images/yunyoseob/post/f45c019a-de65-4cd9-b0dc-96d1aec0b9f8/image.png)

java.io.BufferedInputStream의 constructers를 보시면, 

BufferedInputStream(InputStream in)이 있습니다.

InputStream 참조변수를 입력하여 생성자를 생성하는 것을 의미합니다.

```java
BufferedInputStream inbuf=new BufferedInputStream(fis);
```

> **method**

![](https://images.velog.io/images/yunyoseob/post/63eb918c-58ab-4933-a68f-762fbc9f2165/image.png)

java.io.BufferedInputStream의 methods 중에 read() 함수를 통해 파일의 특정 byte를 읽을 수 있습니다.

## BufferedOutputStream 

> **Constructor**

![](https://images.velog.io/images/yunyoseob/post/7da3882b-8bcd-4fa8-953a-3a02e73bff05/image.png)

java.io.BufferedOutputStream의 constructers를 보시면, 

BufferedOutputStream(OutputStream out)이 있습니다.

OutputStream 참조변수를 입력하여 생성자를 생성하는 것을 의미합니다.


> **method**

![](https://images.velog.io/images/yunyoseob/post/d6e841b5-d026-4ea5-aaf4-f98cbd165df7/image.png)

java.io.BufferedOutputStream의 methods 중에 
write(int b) 함수를 통해 파일의 특정 byte를 작성할 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/b4487c87-d28e-44f4-9fb0-cbb5e1453d9b/image.png)

java.io.BufferedOutputStream의 methods 중에 
flush() 함수를 통해 버퍼된 출력 스트림을 플러시 할 수 있습니다.



## java.io (Input, Output) 예제

> **예제 1**

```java

package a.b.c.prac1;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class BufferStream_p {

	public static void main(String[] args) {
		String inFile=입력할 파일의 절대경로 + "/"+ 파일이름";
		String outFile=작성할 파일의 절대경로 + "/"+ 파일이름";
			
		BufferedInputStream inbuf=null;
		BufferedOutputStream outbuf=null;
		FileInputStream fis=null;
		FileOutputStream fos=null;
		File f=null;
		int data=0;
		
		try {
			f=new File(inFile);
			
			// 파일이 있는지 여부 체크하는 boolean
			boolean bFile=f.exists();
            System.out.println("boolean bFile >>> : "+bFile);
			
			if(bFile){
				// 파일을 읽기 위해서
				fis=new FileInputStream(f);
				inbuf=new BufferedInputStream(fis);
				
				// 파일을 쓰기 위해서
				fos=new FileOutputStream(outFile, true);
				outbuf=new BufferedOutputStream(fos);
				
				// 파일을 읽어서 파일에 쓰기
				while((data=inbuf.read())!=-1){
					System.out.print((char)data);
					outbuf.write(data);
				}
				outbuf.flush();
							
				outbuf.close(); outbuf=null;
				inbuf.close(); inbuf=null;

				fos.close(); fos=null;
				fis.close(); fis=null;		
			}else{
				System.out.println("사용하려는 해당 데이터(파일)이 없습니다.");
			}
		}catch(Exception e){
			System.out.println("error >>>  : "+e.getMessage());
		}finally{
			if (inbuf != null){
				try{inbuf.close(); inbuf=null;}catch(Exception e){}	
			}
			if (outbuf !=null){
				try {outbuf.close(); outbuf=null;}catch(Exception e){}
			}
			if (fis!=null){
				try{fis.close(); fis=null;}catch(Exception e){}
			}
			if (outFile !=null){
				try {fos.close(); fos=null;}catch(Exception e){}
			}
			
		}
		

	}

}
```

> **예제 1 설명**

|명령어|설명|
|--|--|
|f=new File(inFile);|inFile 경로를 File클래스에 인스턴스합니다.|
|boolean bFile=f.exists();|파일이 존재하는지 그렇지 않은지 체크합니다.|
|fis=new FileInputStream(f);|파일을 FileInputSteam(File file)생성자로 인스턴스합니다.|
|inbuf=new BufferedInputStream(fis);|참조변수 fis를 BufferedInputStream(InputStream in)생성자로 인스턴스합니다.|
|fos=new FileOutputStream(outFile, true);|파일경로+파일이름을 FileOutputStream(String name, boolean append)생성자에 인스턴스합니다.|
|outbuf=new BufferedOutputStream(fos);|참조변수 fos를 BufferedOutputStream(OutputStream out)생성자로 인스턴스합니다.
|while((data=inbuf.read())!=-1)||더 이상 파일의 특정 byte를 읽지 못 할때 까지 읽습니다.|
|System.out.print((char)data);|각 data를 char로 자료형 변환을 하여 출력시킵니다.|
|outbuf.write(data);|파일의 특정 byte를 작성합니다.|
|outbuf.flush();|flush() 함수를 통해 버퍼된 출력 스트림을 플러시합니다.|

**추가설명**

✔ FileInputStream(f), BufferedInputStream(fis), FileOutputStream(outFile,     
   true), BufferedOutputStream(fos) 순으로 파일을 IN하고 OUT하였습니다.

✔ close할 때에는 BufferedOutputStream(fos), BufferedInputStream(fis), 
  FileOutputStream(outFile, true), FileInputStream(f) 순으로 닫아준뒤, null로 초기   화 해줍니다. (finally 구문에서 한 번더 !=null로 체크하여 닫히지 않거나, null이 아닌 경   우 한 번 더 close하고 null로 초기화해줍니다.)

> **예제 2**

```java
package a.b.c.prac1;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class InOutStrReadTest_p {

	public static void main(String[] args) {
		String inFile=입력할 절대경로+파일명;
		String outFile=작성할 절대경로+파일명;
		
		File ff=null;
		FileInputStream fis=null;
		FileOutputStream fos=null;
		InputStreamReader isr=null;
		OutputStreamWriter osw=null;
		BufferedReader br=null;
		BufferedWriter bw=null;
		
		int data=0;
		boolean bFile=false;
		
		try{
			ff=new File(inFile);
			bFile=ff.exists();
			System.out.println("ff.exists() (bFile) >>> : "+bFile);
			
			if(bFile){
				fis=new FileInputStream(ff);
				isr=new InputStreamReader(fis);
		
				br=new BufferedReader(isr);
				
				fos=new FileOutputStream(outFile);				
				osw=new OutputStreamWriter(fos);
				
				bw=new BufferedWriter(osw);
				
				while((data=br.read()) !=-1){
					System.out.print((char)data);
					bw.write(data);
				}
				bw.flush();
			}else{
				System.out.println("해당 경로에 파일이 존재하지 않습니다. >>> : ");
			}

			bw.close(); bw=null;
			br.close(); br=null;
			
			osw.close(); osw=null;
			isr.close(); isr=null;
			
			fos.close(); fos=null;
			fis.close(); fis=null;
			
		}catch(Exception e){
			System.out.println("error >>> : "+e.getMessage());
			
		}finally{
			if(bw!=null){
				try{bw.close(); bw=null;}catch(Exception e){}
				}
			if(br!=null){
				try{br.close(); br=null;}catch(Exception e){}
				}
			if(osw!=null){
				try{osw.close(); osw=null;}catch(Exception e){}
				}
			if(isr!=null){
				try{isr.close(); isr=null;}catch(Exception e){}
				}
			if(fos!=null){
				try{fos.close(); fos=null;}catch(Exception e){}
				}
			if(fis!=null){
				try{fis.close(); fis=null;}catch(Exception e){}
				}		
		}
	}

}
```

> **예제 2 설명**

**Input, Output 이외에도 Reader와 Writer를 활용할 수도 있습니다.**

**추가설명**

✔ FileInputStream(ff), InputStreamReader(fis), BufferedReader(isr),

  FileOutputStream(outFile), OutputStreamWriter(fos), BufferedWriter(osw) 

  순으로 파일을 IN하고 OUT하였습니다.

✔ close할 때에는 BufferedWriter, BufferedReader, OutputStreamWriter, 

  InputStreamReader, FileOutputStream, FileInputStream 순으로 닫아 줍니다.  

  (finally 구문에서 한 번더 !=null로 체크하여 닫히지 않거나, null이 아닌 경우한 번 더   close하고 null로 초기화해줍니다.)



**이상으로 java.io에 대한 포스팅을 마치도록 하겠습니다. 😀**
