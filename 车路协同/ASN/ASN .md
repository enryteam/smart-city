[TOC]

ASN.1[抽象语法标记](https://baike.baidu.com/item/抽象语法标记/3024369)（Abstract Syntax Notation One） ASN.1是一种 ISO/ITU-T 标准，描述了一种对数据进行表示、[编码](https://baike.baidu.com/item/编码/80092)、传输和解码的数据格式。它提供了一整套正规的格式用于描述对象的结构，而不管语言上如何执行及这些数据的具体指代，也不用去管到底是什么样的应用程序。



# 一、简介

在任何需要以数字方式发送信息的地方，ASN.1  都可以发送各种形式的信息（声频、视频、数据等等）。ASN.1 和特定的 ASN.1  编码规则推进了结构化数据的传输，尤其是网络中应用程序之间的结构化数据传输，它以一种独立于计算机架构和语言的方式来描述数据结构。



OSI 协议套中的[应用层协议](https://baike.baidu.com/item/应用层协议/3668945)使用了 ASN.1 来描述它们所传输的 PDU，这些协议包括：用于传输电子邮件的 X.400、用于[目录服务](https://baike.baidu.com/item/目录服务)的 X.500、用于 VoIP 的 H.323 和 SNMP。它的应用还可以扩展到[通用移动通信系统](https://baike.baidu.com/item/通用移动通信系统)（UMTS）中的接入和[非接入层](https://baike.baidu.com/item/非接入层/5876110)。

ASN.1  取得成功的一个主要原因是它与几个标准化编码规则相关，如基本编码规则（BER） -X.209  、规范编码规则（CER）、识别名编码规则（DER）、压缩编码规则（PER）和 XML编码规则（XER）。这些编码规则描述了如何对 ASN.1  中定义的数值进行编码，以便用于传输，而不管计算机、编程语言或它在应用程序中如何表示等因素。ASN.1  的编码方法比许多与之相竞争的标记系统更先进，它支持可扩展信息快速可靠的传输 — 在无线宽带中，这是一种优势。1984年，ASN.1  就已经成为了一种国际标准，它的编码规则已经成熟并在可靠性和兼容性方面拥有更丰富的历程。

简洁的[二进制编码](https://baike.baidu.com/item/二进制编码/1758517)规则（BER、CER、DER、PER，但不包括 XER）可当作更现代 XML 的替代。然而，ASN.1 支持对数据的语义进行描述，所以它是比 XML 更为高级的语言。

正是由于这种数据类型的“抽象"特性，所以描述它的语法在OSI术语中被称为抽象语法（abstract syntax).抽象语法定义的数据类型，在传输时遵循的数据编码规则，称为传输语法(transfer  syntax).一种ASN.1数据类型对应的传输语法可以有多种，但只能使用其中的一种。

ASN.1 的描述可以容易地被映射成 C 或 C++ 或 Java 的数据结构，并可以被应用程序代码使用，并得到运行时[程序库](https://baike.baidu.com/item/程序库)的支持，进而能够对编码和解码 XML 或 TLV 格式的，或一种非常紧凑的压缩编码格式的描述。

同时，ASN.1也是一种用于描述结构化客体的结构和内容的语言。

![image-20210609091117500](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210609091117500.png)



# 二、定义

[抽象语法](https://baike.baidu.com/item/抽象语法)定义:

ASN.1是描述在网络上传输信息格式的标准方法。它有两部分：一部分描述信息内数据，数据类型及序列格式；另一部分描述如何将各部分组成消息。它原来是作为X.409的一部分而开发的，后来才自己独立成为一个标准。ASN.1在OSI的ISO 8824/ITU X.208（说明语法）和ISO 8825/ITU X.209（说明基本编码规则）规范。

例如：

```ASN.1
Report ::= SEQUENCE {
    author OCTET STRING,
    title OCTET STRING,
    body OCTET STRING,
    biblio Bibliography
}
```



在这个例子中，"Report"是由名字类型的信息组成的，而SEQUENCE表示消息是许多[数据单元](https://baike.baidu.com/item/数据单元)构成的，前三个数据单元的类型是OCTET STRING，而最后一个数据类型见下面的ASN.1语法表示它的意义：

```ASN.1
Bibliography ::= SEQUENCE {
    author OCTET STRING
    title OCTET STRING
    publisher OCTET STRING
    year OCTET STRING
}
```



# 三、数据类型

ASN.1 提供了一些基本的预定义数据类型：

![img](https://img-blog.csdn.net/2018022515255454)

```ASN.1
UNIVERSAL 0 保留给编码规则使用
UNIVERSAL 1布尔类型
UNIVERSAL 2[整型](https://baike.baidu.com/item/整型)
UNIVERSAL 3零或多个比特的序列
UNIVERSAL4 零或多个字节的序列
UNIVERSAL5 NULL
UNIVERSAL 6 对象[标识符](https://baike.baidu.com/item/标识符)类型
UNIVERSAL 7 对象描述符类型
UNIVERSAL 8 外部类型和类型实例
UNIVERSAL 9 实数类型
UNIVERSAL 10 枚举类型
UNIVERSAL 11 嵌入的 pdv 类型
UNIVERSAL 12 UTF8 字符串类型
UNIVERSAL 13 相关对象标识符类型
UNIVERSAL 14-15 保留给本建议的以后版本和国际标准使用
UNIVERSAL 16 序列和类型序列
UNIVERSAL 17 集合和类型的集合
UNIVERSAL 18-22, 25-30 字符串 类型
UNIVERSAL 23-24 时间 类型
UNIVERSAL 31-... 保留给本建议以外的类型和[国际标准](https://baike.baidu.com/item/国际标准)使用
```



# 四、数据结构

ASN.1 还能够定义如下的数据结构类型：

- 结构 ( SEQUENCE )

- 列表 ( SEQUENCE OF )

- 类型选择 ( CHOICE )



# 五、ASN.1模块定义

一般协议有一个或者多个模块组成，模块用来收集数据结构定义，模块必须以大写字母开头，能以一种全局指针的方式来引用，成为对象标识符，用花括号标识在名字之后。

![img](https://img-blog.csdn.net/20180225152715940)

# 六、Java中使用ASN.1

每一项的格式都是固定:

> tag + 长度+具体内容

java类sun.security.util.DerValue中一下标签

```java
 public final static byte    tag_Boolean = 0x01;
 public final static byte    tag_Integer = 0x02;
 public final static byte    tag_BitString = 0x03;
 public final static byte    tag_OctetString = 0x04;
 public final static byte    tag_Null = 0x05;
 public final static byte    tag_ObjectId = 0x06;
 public final static byte    tag_Enumerated = 0x0A;
 public final static byte    tag_UTF8String = 0x0C;
 public final static byte    tag_PrintableString = 0x13;
 public final static byte    tag_T61String = 0x14;
 public final static byte    tag_IA5String = 0x16;
 public final static byte    tag_UtcTime = 0x17;
 public final static byte    tag_GeneralizedTime = 0x18;
 public final static byte    tag_GeneralString = 0x1B;
 public final static byte    tag_UniversalString = 0x1C;
 public final static byte    tag_BMPString = 0x1E;
 public final static byte    tag_Sequence = 0x30;
 public final static byte    tag_SequenceOf = 0x30;
 public final static byte    tag_Set = 0x31;
 public final static byte    tag_SetOf = 0x31;
```



java的sun.security.util包中提供的DerInputStrem和DerOutputStream可以用于读写ASN格式。

```java
BigInteger int1=new BigInteger("1234567812345678");
BigInteger int2=new BigInteger("123456789123456789");
DerOutputStream dout=new DerOutputStream();
dout.putInteger(int1);
dout.putInteger(int2);
DerOutputStream sequence=new DerOutputStream();
sequence.write(DerValue.tag_Sequence, dout);
HexDumpEncoder encoder=new HexDumpEncoder();
byte[] result=sequence.toByteArray();
System.out.println(encoder.encode(result));

DerInputStream din=new DerInputStream(result);
DerValue[] value=din.getSequence(0);
System.out.println(value[0].getBigInteger());
DerInputStream din2=new DerInputStream(value[1].toByteArray());
System.out.println(din2.getBigInteger());
```

输入结果为：

```java
0000: 30 13 02 07 04 62 D5 37   E7 EF 4E 02 08 01 B6 9B  0....b.7..N.....
0010: 4B AC D0 5F 15 
1234567812345678
123456789123456789
```