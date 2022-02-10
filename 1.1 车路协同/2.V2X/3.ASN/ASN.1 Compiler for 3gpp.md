- [ASN.1 Compiler for 3gpp](https://blog.csdn.net/weixin_39920581/article/details/86692189)

ASN.1，指抽象语法标记（Abstract Syntax Notation One），是一种 ISO/ITU-T 标准，描述了一种对数据进行表示、编码、传输和解码的数据格式。它提供了一整套正规的格式用于描述对象的结构，而不管语言上如何执行及这些数据的具体指代，也不用去管到底是什么样的应用程序[摘抄自百度百科，不是本文要说的重点]。

标准的ASN.1编码规则有基本编码规则（BER，Basic Encoding Rules）、唯一编码规则（DER，Distinguished Encoding Rules）、压缩编码规则（PER，Packed Encoding Rules）和XML编码规则（XER，XML Encoding Rules），本文就自己学习的PER/UPER编码做相关总结！

PER (压缩编码规则) 分为:对齐方式(Aligned PER，APER)与非对齐方式(Unaligned PER,UPER)两种情况,两者的关键区别是，APER编码指在对一串数据进行编码时，要求对每一个数据格式的编码（完成以后）都要进行八位（8bit）对齐操作，即需要高位或者低位补0操作；UPER编码指在对一串数据进行编码时，只在全部数据编码结束后才进行八位（8bit）对齐操作。

针对UPER编码，根据ASN.1中的数据结构类型，可分类列出每种数据结构的UPER编码规则。

UPER的编码原则是:用尽可能简单的规则得到最简洁的编码。

根绝X.680协议，ASN.1的数据类型主要有以下几种：

1）简单类型：a.BOOLEAN(布尔类型，只有真假两个值),b.NULL(空),c.INTEGER(整形，可表示任意长度的整数),d.ENUMERATED(枚举类型),e.BIT STRING(位串，代表以比特为单位的二进制字符串),f.OCTET STRING(八位串，代表以自己为单位的二进制字符串)；

2）复合类性：g.CHIOCE(选择类型，可表示每次选择数据类型中的一个),h.SEQUENCE(序列，可表示一组不同数据类型的集合，=c中struct),I.SEQUENCE OF (可表示定义了同一数据类型元素的集合，=c中数组),j.SET(同SEQUENCE), k.SET OF (同SEQUENCE OF)；

在最新的X.691协议中给出了以上每种类型的编码方式，本文是对对691协议中编码方式的整理及实例验证，并且着重对扩展标记“...”存在问题进行研究，因为针对最新的5G 3GPP协议中涉及到的ASN.1结构，相对4G有了一些扩展及改变，本文的研究可以更好的对5G 3GPP协议中涉及到的ASN.1结构的编码实现。

接下来本文对以上a-k种数据类型，分别按照基本定义/691协议编码内容/流程图/编码实例等步骤进行讲解，