- ASN.1是什么？
   ASN.1抽象语法标记（Abstract Syntax Notation One）  ASN.1是一种 ISO/ITU-T  标准，描述了一种对数据进行表示、编码、传输和解码的数据格式。它提供了一整套正规的格式用于描述对象的结构，而不管语言上如何执行及这些数据的具体指代，也不用去管到底是什么样的应用程序。
- 本人在工作中涉及到ASN.1结构的场景
   证书的公、私钥文件，做数据加密、签名、信封产生的数据都是ASN.1结构。
- 解析ASN.1
   下面是一段简单的解析ASN.1结构，获取ASN.1结构的元素类型和值的代码。
   如有图片中三种ASN.1结构的数据，要判断是其中的哪一种格式：
   [![在这里插入图片描述](https://img.it610.com/image/info8/1b1db4ec4fc5413dac7d87624a0ee1d2.png)](https://img.it610.com/image/info8/1b1db4ec4fc5413dac7d87624a0ee1d2.png)[![在这里插入图片描述](https://img.it610.com/image/info8/a9185958a3324b1fa344c9b82a9b0f98.png)](https://img.it610.com/image/info8/a9185958a3324b1fa344c9b82a9b0f98.png)[![在这里插入图片描述](https://img.it610.com/image/info8/184e09e4579e442e98cb4a243cd09bce.png)](https://img.it610.com/image/info8/184e09e4579e442e98cb4a243cd09bce.png)

```java
/**
	 * 获取sequence下第一个元素，并判断元素类型
	 * @param data
	 * @return
*/
private static String read_Asn1Data(byte[] data) {
		ByteArrayInputStream bis = null;
		ASN1InputStream ais = null;
		String flag = "";
		try {
			bis = new ByteArrayInputStream(data);
			ais = new ASN1InputStream(bis);
			DERSequence sequence = (DERSequence) ais.readObject();
			DEREncodable derEnd  = sequence.getObjectAt(0);
			DERObject readObject = derEnd.getDERObject();
			if (readObject instanceof DERSequence) {
				flag = "0";
			}else if (readObject instanceof DERInteger) {
				flag = "1";
			}else if (readObject instanceof DERObjectIdentifier){
				flag = "2";
			}
		} catch (IOException e) {
		} finally {
			try {
				if (bis != null) bis.close();
				if (ais != null) ais.close();
			} catch (IOException e) {}
		}
		return flag;
	}
/**
	 * 获取元素值
	 * @param data
	 * @return
*/
private static String read_Asn1Data(byte[] data) throws Exception {
		ByteArrayInputStream bis = null;
		ASN1InputStream ais = null;
		ContentInfo contentInfo = null;
		try {
			bis = new ByteArrayInputStream(data);
			ais = new ASN1InputStream(bis);
			contentInfo = new ContentInfo((ASN1Sequence) ais.readObject());
		} catch (IOException e) {
			throw e;
		} finally {
			try {
				if (bis != null) bis.close();
				if (ais != null) ais.close();
			} catch (IOException e) {}
		}
		return contentInfo.getContentType().getId();
	}
```

# 将java转化为ASN.1、转base64、以十六进制输出；再解析ASN.1。(BC中的ASN1组装和解析)

实习小任务

 要求：

1.写一个Java对象；

2.转化为ASN.1类型（包括ASN1Integer、ASN1Boolean、ASN1String、ASN1Sequence）;

3.转换为byte[]、编码为base64；

4.最后以十六进制输出。

 以下为代码： 

pom.xml：

```xml
<dependency>
	<groupId>org.bouncycastle</groupId>
	<artifactId>bcprov-ext-jdk15on</artifactId>
	<version>1.51</version>
</dependency>
```


​         

Asn1Entity对象：

```java
package com.xdja.timingDemo.model;
 
import org.bouncycastle.asn1.*;
 
public class Asn1Entity extends ASN1Object {
 
    //整数
    private ASN1Integer asn1Integer ;
    //String类型
    private DERUTF8String derutf8String;
    //布尔型
    private DERBoolean derBoolean ;
    //集合、组合
    private ASN1Sequence asn1Sequence;
 
    public Asn1Entity(ASN1Integer asn1Integer, DERUTF8String derutf8String, DERBoolean derBoolean,ASN1Sequence asn1Sequence) {
        this.asn1Integer = asn1Integer;
        this.derutf8String = derutf8String;
        this.derBoolean = derBoolean;
        this.asn1Sequence = asn1Sequence;
 
    }
    //get、set省略
 
    @Override
    public ASN1Primitive toASN1Primitive() {
        //传值
        ASN1EncodableVector vector = new ASN1EncodableVector();
        vector.add(asn1Integer);
        vector.add(derutf8String);
        vector.add(derBoolean);
        vector.add(asn1Sequence);
        return new DERSequence(vector);
 
    }
}
```

java转ASN.1:

```java
package com.xdja.timingDemo.asn1;
 
import com.xdja.timingDemo.model.Asn1Entity;
import org.bouncycastle.asn1.*;
 
import java.io.IOException;
import java.math.BigInteger;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Date;
import java.util.List;
 
public class TestAsn1 {
 
    public static List sequence() {
 
        Integer id = 1;
        Boolean status = true;
        String name = "学习强国";
 
        List<String> list = new ArrayList();
        list.add("ocsp");
        list.add("asn.1");
        list.add("java");
        list.add("base64");
 
        ASN1EncodableVector asn1EncodableVector = new ASN1EncodableVector();
        for (String s : list) {
            asn1EncodableVector.add(new DERUTF8String(s));
        }
        asn1EncodableVector.add(new ASN1Integer(999));
        asn1EncodableVector.add(new DERUTCTime(new Date()));
        System.out.println("size:" + asn1EncodableVector.size());
 
        //构造函数
        Asn1Entity asn1Entity = new Asn1Entity(new ASN1Integer(id), new DERUTF8String(name), new DERBoolean(status), new DERSequence(asn1EncodableVector));
 
        //asn1Entity 转换byte[]
        byte[] encode = null;
        try {
            encode = asn1Entity.toASN1Primitive().getEncoded();
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println("encode----------" + Arrays.toString(encode));
        //byte[]转BASE64
        byte[] b64 = org.bouncycastle.util.encoders.Base64.encode(encode);
        System.out.println("base64----------" + Arrays.toString(b64));
        //b64转换十六进制
        String str = new BigInteger(1, b64).toString(16);
        System.out.println("16进制----------" + str);
             
        return null;
    }
 
    public static void main(String[] args) {
        TestAsn1.sequence();
 
    }
}
```

ASN.1解析：

```java
        //解码为byte数组
        byte[] d64 = org.bouncycastle.util.encoders.Base64.decode(b64);
        System.out.println("decode----------" + Arrays.toString(d64));
        System.out.println("---------------------------------------------------------");
        ASN1InputStream asn1InputStream = new ASN1InputStream(d64);
        ASN1Primitive asn1Primitive;
        try {
            //asn1Entity看作一个组合
            while ((asn1Primitive = asn1InputStream.readObject()) != null) {
                    ASN1Sequence asn1Sequence = (ASN1Sequence) asn1Primitive;
                    ASN1SequenceParser asn1SequenceParser = asn1Sequence.parser();
                    ASN1Encodable asn1Encodable;
                    while ((asn1Encodable = asn1SequenceParser.readObject()) != null) {
                        asn1Primitive = asn1Encodable.toASN1Primitive();
 
                        if (asn1Primitive instanceof DERUTF8String) {
                            DERUTF8String string = (DERUTF8String) asn1Primitive;
                            System.out.println("DERUTF8String--:" + string.getString());
                        } else if (asn1Primitive instanceof ASN1Boolean) {
                            ASN1Boolean asn1Boolean = (ASN1Boolean) asn1Primitive;
                            System.out.println("ASN1Boolean--:" + asn1Boolean.toString());
                        } else if (asn1Primitive instanceof ASN1Integer) {
                            ASN1Integer asn1Integer = (ASN1Integer) asn1Primitive;
                            System.out.println("ASN1Integer--:" + asn1Integer.getValue());
                        }else{
 
                            ASN1Sequence asn1Sequence1 = (ASN1Sequence) asn1Primitive;
                            ASN1SequenceParser asn1SequenceParser1 = asn1Sequence1.parser();
                            ASN1Encodable asn1Encodable1;
 
                            while ((asn1Encodable1 = asn1SequenceParser1.readObject()) != null) {
                                asn1Primitive = asn1Encodable1.toASN1Primitive();
 
                                if (asn1Primitive instanceof DERUTF8String) {
                                    DERUTF8String string = (DERUTF8String) asn1Primitive;
                                    System.out.println("DERUTF8String--:" + string.getString());
                                }else if (asn1Primitive instanceof ASN1UTCTime) {
                                    ASN1UTCTime asn1utcTime = (ASN1UTCTime) asn1Primitive;
                                    System.out.println("UTCTime:"+asn1utcTime.getTime());
                                }
 
                            }
 
                        }
 
                    }
 
            }
        } catch (Exception e) {
            e.printStackTrace();
 
        }
```

输出：

![img](https://img-blog.csdnimg.cn/20190305115852931.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjIwOTM2OA==,size_16,color_FFFFFF,t_70)

# Java对asn.1格式数据编解码示例

  工作中用到了asn.1格式数据，所以这里对asn.1格式的编解码做一个简单的介绍，主要通过程序来构建与解析asn.1格式数据。asn.1格式一般分为三个部分，分别是类型、长度、值，也就是Tag,Length,Value，简称TLV格式。

    类型一般分为以下几种：
    sequence，也叫集合和结构
    integer，整数
    utf8string，字符串
    boolean，布尔类型
    time，时间类型
下面构建一个maven项目，引入项目依赖：

```xml
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcprov-ext-jdk15on</artifactId>
    <version>1.65</version>
</dependency>
```

定义一个student的实体类，继承ASN1Object：

```java
package com.xxx.asn1;
 
import org.bouncycastle.asn1.ASN1EncodableVector;
import org.bouncycastle.asn1.ASN1Integer;
import org.bouncycastle.asn1.ASN1Object;
import org.bouncycastle.asn1.ASN1Primitive;
import org.bouncycastle.asn1.DERSequence;
import org.bouncycastle.asn1.DERUTF8String;
import org.bouncycastle.asn1.x509.Time;
 
public class Student extends ASN1Object {
	
	private ASN1Integer id;
	private DERUTF8String name;
	private ASN1Integer age;
	private Time createDate;
	
	public void setId(ASN1Integer id) {
		this.id = id;
	}
	public void setName(DERUTF8String name) {
		this.name = name;
	}
	public void setAge(ASN1Integer age) {
		this.age = age;
	}
	public void setCreateDate(Time createDate) {
		this.createDate = createDate;
	}
	
	public ASN1Integer getId() {
		return id;
	}
	public DERUTF8String getName() {
		return name;
	}
	public ASN1Integer getAge() {
		return age;
	}
	public Time getCreateDate() {
		return createDate;
	}
	
	public Student() {
		// TODO Auto-generated constructor stub
	}
	
	
 
	public Student(ASN1Integer id, DERUTF8String name, ASN1Integer age,
			Time createDate) {
		super();
		this.id = id;
		this.name = name;
		this.age = age;
		this.createDate = createDate;
	}
	
	@Override
	public ASN1Primitive toASN1Primitive() {
		ASN1EncodableVector vector = new ASN1EncodableVector();
		vector.add(id);
		vector.add(name);
		vector.add(age);
		vector.add(createDate);
		return new DERSequence(vector);
	}
 
}
```

 定义一个主类App，来分别构建asn.1和解析asn.1格式数据：

```java
package com.xxx.asn1;
 
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Date;
 
import org.bouncycastle.asn1.ASN1Encodable;
import org.bouncycastle.asn1.ASN1InputStream;
import org.bouncycastle.asn1.ASN1Integer;
import org.bouncycastle.asn1.ASN1Primitive;
import org.bouncycastle.asn1.ASN1Sequence;
import org.bouncycastle.asn1.ASN1SequenceParser;
import org.bouncycastle.asn1.DERUTF8String;
import org.bouncycastle.asn1.x509.Time;
import org.bouncycastle.util.encoders.Base64;
 
public class App {
	
	/**
	 * 构建asn.1
	 */
	public static void buildStudent(){
		Integer id = 1;
    	String name = "buejee";
    	Integer age = 18;
    	Time createDate = new Time(new Date());
    	try {
			
    		Student student = new Student(new ASN1Integer(id),
    				new DERUTF8String(name),
    				new ASN1Integer(age),
    				createDate);
    		String data = Base64.toBase64String(student.getEncoded());
    		System.out.println(data);
    		OutputStream out = new FileOutputStream(new File("student.cer"));
    		out.write(data.getBytes());
    		out.flush();
    		out.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * 解析asn.1
	 */
	public static void resolveStudent(){
		byte[] data = Base64.decode("MB0CAQEMBmJ1ZWplZQIBEhcNMjAwNTE1MTUxNDAzWg==");
		ASN1InputStream ais = new ASN1InputStream(data);
		ASN1Primitive primitive = null;
		try {
			while((primitive=ais.readObject())!=null){
				System.out.println("sequence->"+primitive);
				if(primitive instanceof ASN1Sequence){
					ASN1Sequence sequence = (ASN1Sequence)primitive;
					ASN1SequenceParser parser = sequence.parser();
					ASN1Encodable encodable = null;
					while((encodable=parser.readObject())!=null){
						primitive = encodable.toASN1Primitive();
						System.out.println("prop->"+primitive);
					}
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
			try {
				ais.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	
    public static void main( String[] args ){
    	//buildStudent();
    	resolveStudent();
    }
}
```

 分别运行两个方法，第一个是buildStudent()是构建一个asn.1格式数据，我们最后将他转为base64字符串，打印并存储在student.cer文件中。

![img](https://img-blog.csdnimg.cn/20200515233906852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

 打印的结果和保存在student.cer中的结果是一样的。我们可以通过asn1view工具查看这个内容：

  sequence部分：

![img](https://img-blog.csdnimg.cn/20200515235341272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

第一个integer:

![img](https://img-blog.csdnimg.cn/20200515235400229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

 string:

![img](https://img-blog.csdnimg.cn/20200515235420649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

 第二个integer:

![img](https://img-blog.csdnimg.cn/20200515235434893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

  time :

![img](https://img-blog.csdnimg.cn/20200515235502395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZlaW5pZmk=,size_16,color_FFFFFF,t_70)

这所有的内容都符合我们在代码中定义的数据：

![img](https://img-blog.csdnimg.cn/20200515235729127.png)

   id=1,name=buejee,age=18,createDate=(20)20/05/15 15:36:43,时间是世界时间，所以东八区的话应该是(20)20/05/15 23:36:43，都是正确的。

    我们再来看看解析，调用resolveStudent()方法，控制台打印结果如下：
![img](https://img-blog.csdnimg.cn/2020051600011121.png)

 数据读出来了。跟我们构建时传入的参数一样。

  本文的代码和工具asn1view都会放到[github](https://github.com/buejee/asn1demo)上，有需要的可以查看。 