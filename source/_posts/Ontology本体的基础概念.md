---
title: Ontology本体的基础概念
categories:
  - 什么都学一下
  - 学习log
tags:
  - ontology
  - 本体
  - 本体论
id: 273
date: 2013-07-15 01:37:51
---

#### 本体论基础&amp;概念

        本体作为一种能在语义和知识层次上描述领域概念的建模工具，其目标是捕获相关领域的知识，确定该领域内共同认可的词汇，通过概念之间的关系来描述概念的语义，提供对该领域知识的共同理解。语义Web（the Semantic Web）是在本体理论基础之上对现有Web所进行的扩展[15]，其目标是使Web上的信息具有计算机可以理解的语义，在本体的支持下实现信息系统间语义上的互操作性，以及对Web资源所进行的智能访问和检索[16]。充分实现语义Web的潜力，需要大规模采用基于本体的方法来共享信息和资源，本体是语义Web得以实现的基础和关键。

*   ##### **<span style="color: #49352f; font-family: 'Poiret One', 'Times New Roman', serif; font-size: 21px; line-height: 15px;">本体（Ontology）</span>**

本体是共享概念模型的明确的形式化规范说明（An ontology is a formal, explicit specification of a shared conceptualisation.）”。该定义包含四层含义：

1）概念模型（Conceptualization），即本体是通过抽象客观世界的概念而得到的模型，它表示的含义独立于具体的环境状态；

2）明确性（Explicit），即本体所使用的概念及在这些概念之上的约束都有明确的定义，没有二义性；

3）形式化（Formal），即本体是计算机可处理的，而不是自然语言；

 4）共享（Shared），即本体体现的是共同认可的知识，反映的是相关领域中公认的概念集合，它所针对的是团体而不是个体。

*   ##### **<span style="line-height: 15px;">本体建模元素</span>**

1)类（Classes）或概念（Concepts）

        其含义非常广泛，指任何事务，如工作描述、功能、行为、策略和推理过程。从语义上讲，它表示的是对象的集合，其定义包括概念的名称，与其他概念之间的关系的集合，以及用自然语言对概念的描述。

2)关系（Relations）

        在领域中概念之间的交互作用，形式上定义为n维笛卡儿积的子集。如子类关系（subClassOf）。在语义上关系对应于对象元组的集合。

3)函数（Functions）

        一类特殊的关系。该关系的前n－1个元素可以唯一决定第n个元素。形式化的定义为F: C1×C2×…×Cn-1→Cn。如motherOf就是一个函数，motherOf(x, y)表示y是x的母亲。

4)公理（Axioms）

        代表永真断言，如概念乙属于概念甲的范围。

5)实例（Instances）

        代表某概念类的基本元素，即某概念类所指的具体实体。从语义上讲实例表示的就是对象。

*   **<span style="line-height: 15px;">概念间关系</span>**

        概念间的关系可以分为两类：分类关系和非分类关系，包括4种类型，part-of——表达概念之间部分与整体的关系、kind-of——表达概念之间的继承关系，类似于面向对象中的子类和父类之间的关系、instance-of——表达概念之间的实例和概念之间的关系、attribute-of——表达某个概念是另外一个概念的属性。

        Gruber提出了根据特定领域构造本体的准则：

       （1）清晰性、明确性和客观性：即本体应该用自然语言对所定义的术语给出明确的、客观的语义定义，有效的说明所定义术语的含义。而且，当定义可以用逻辑公理表达时，它应该是形式化的。

        （2）完全性：即所给出的定义是完整的，完全能表达所描述术语的含义。

        （3）一致性：即由术语得出的推论与术语本身的含义是相容的，支持与其定义相一致的推理，不会产生矛盾。

        （4）最大单调可拓展性：即向本体中添加通用或专用的术语时，不需要修改其已有的概念定义和内容，支持在已有的概念基础上定义新术语。

        （5）最小承诺和最小编码偏好：所谓最小承诺，即本体约定应该最小，对待建模对象应给出尽可能少的约束。对编码偏好应该是最小化的，因为不同的知识系统可能采用不同的表达方法或表示风格。

        以上5条是最具影响力的，其余几条准则分别是：

（6）本体描述原则（Ontological Distinction Principle）[36]：本体中的类应该是互不相交的。

（7）概念层次多样化（Diversification of hierarchies）增强多继承机制的能力[37]。

（8）模块化设计（Modularity）以最小化模块化之间的耦合度[38]。

（9）语义距离最小化（Minimization of the semantic distance）[37]：兄弟概念之间的语义距离最小化，尽可能把含义相似的概念抽象出来，用相同的元语来表示。

（10）命名标准化（Standardization of names）[37]：尽可能使用标准的名字。

*   ##### **<span style="line-height: 28px;">Web3.0和语义网</span>**

        互联网专家们认为，对于普通用户而言，Web 3.0带来的最大好处就是让你拥有了一个贴身的私人助理。根据专家们的观点，Web3.0时代网络对你无所不知，能够自主地查询互联网上的所有信息来回答任何问题。许多专家把Web 3.0比做是庞大的数据库。Web2.0使用互联网是为了把人与人联系起来，而Web 3.0使用互联网是为了把信息与信息联系起来。一些专家认为Web3.0会取代目前的互联网，另一些专家则认为它将作为独立的网络而存在。

        在Web3.0时代你只要发出一个很简单的指令，剩下的事情则交给互联网，互联网完全可以替你做所有工作：它会根据你的偏好确定搜索参数，以缩小搜索服务的范围。然后，浏览器程序会收集并分析数据并提供给你，便于你进行比较。浏览器之所以有这个本领，是因为Web 3.0能够理解网上的信息。
今天，你使用互联网搜索引擎时，搜索引擎其实并不真正理解你要搜索的东西。它只是简单地查找出现搜索框中的关键字的众多网页，而无法告诉某网页是不是真与你搜索的东西相关。换句话说，它只能告诉你，关键字出现在该网页上。比如，搜索的是“土星”这个词，最后会得到有关土星的网页搜索结果和有关汽车生产商土星公司的其他搜索结果。

        TimBerners-Lee于1989年发明了互联网。他发明的互联网其最主要用途是作为统一的界面实现信息的彼此共享。不过，Berners-Lee对Web2.0到底是否存在表示怀疑，认为它只是毫无意义的专业术语。Berners-Lee坚持认为，他发明互联网就是为了能够让这一网络架构能处理Web2.0所能处理的所有任务。Berners-Lee设想未来的互联网与今天的Web 3.0概念很相似。它被称为语义网(Semantic Web)。
简单地说，今天的互联网架构是为方便人使用而设计的。它让我们容易访问网页，理解网页所呈现的一切，而计算机却不能理解。搜索引擎也许能查找关键字，但它理解不了这些关键字在网页语境下是如何使用的。
有了语义网，计算机将使用软件代理来搜索及理解网页上的信息。这些软件代理将是在互联网上搜索相关信息的程序。它们之所以有这种功能，就是因为语义网拥有信息的集合体，这种集合体就叫本体(ontology)。在互联网上，本体其实是一个文件，它定义了一组词语之间的关系。

        语义网要发挥应有的功效，本体内容就必须详细而全面。按照Berners-Lee的概念，本体会以元数据(元数据是指网页代码中所含的人类看不见而计算机能读取的信息)的形式而存在。
构建本体需要大量的工作。实际上，这是语义网面临的重大障碍之一。人们是否愿意投入精力为自己的网站构建全面完整的本体？网站变化后，他们会维护本体吗？这些都是语义网构建时需要考虑的问题。批评人士认为，创建及维护语义网这种复杂的任务对大多数人来说工作量太大了。
另一方面，一些人很喜欢给互联网对象和信息做标签或做标记。互联网可以对做了标记的对象或信息进行分类。如果博客含有一个标记选项，这样很容易按特定主题对日志内容进行分类。Flickr等照片共享网站让用户可以对照片做标记。

*   ##### **RDF（S）和OWL**

RDF和RDFS作为W3C标准，提供了统一的、形式化的数据表示语言来描述Web上资源的含义。OWL建立在RDF之上，定义了RDF（S）描述中使用的词汇的语法，便于RDF（S）对元数据的处理，是计算机理解Web资源的基础。

一个资源描述模型必须解决三个问题：

1.  资源的标识，即如何标识被描述的资源。该标识系统不能和其它的标识系统混淆，即使面对互联网上千差万别、不计其数的资源也可以用简单、有效的方法进行标识。
2.  <span style="line-height: 28px;">l 结构设计。该模型在结构上要尽可能的简单，易于掌握；同时也应具有一定的灵活性、易于扩展，适于互联网分布式的网状结构。</span>
3.  <span style="line-height: 28px;">l 语言系统。既用可被机器理解的计算机语言对该模型进行描述，表达足够的语义以方便机器之间的交流。</span>

        除此之外，一个资源描述模型在设计时还应考虑与现有标准的兼容、实现的难易程度以及应用前景和价值等方方面面的问题。
RDF模型是一种二元关系模型，它采用URI来标识被描述的资源，通过陈述描述资源。
XML是Web上数据表示的标准，因此RDF采用了一种基于XML语法的语言系统来表示RDF陈述，称为RDF/XML。

—**Resource Description Framework，RDF**

        一种用于描述Web资源的标记语言。RDF是一个处理元数据的XML应用，所谓元数据，就是“描述数据的数据”或者“描述信息的信息”。也许这样解释元数据有些令人难以理解，举个简单的例子，书的内容是书的数据，而作者的名字、出版社的地址或版权信息就是书的元数据。数据和元数据的划分不是绝对的，有些数据既可以作为数据处理，也可以作为元数据处理，例如可以将作者的名字作为数据而不是元数据处理。

       RDF基于这样的思想：用Web标识符（称作统一资源标识符，Uniform Resource Identifiers或URIs）来标识事物，用简单的属性（property）及属性值来描述资源。这使得RDF可以将一个或多个关于资源的简单陈述表示为一个由结点和弧组成的图（graph），其中的结点和弧代表资源、属性或属性值。其中每个陈述都是由**主体**（subject），**谓词**（predicate），**客体**（object）组成的。为了让讨论显得尽量具体一些，下面的这组陈述“有一个人由http://www.w3.org/People/EM/contact#me 标识, 他的名字是Eric Miller, 他的电子邮件地址是em@w3.org,他的头衔是Dr.”可以表示为图1 (http://www.w3.org/TR/2004/REC-rdf-primer-20040210/#figure1)所示的图：

[![27683_2](http://farm8.staticflickr.com/7390/9287033894_d345589db9.jpg)](http://www.flickr.com/photos/ovbeeshoot/9287033894/ "Flickr 上 Liar1992 的 27683_2")

其表达的RDF如以下XML文档所示

<pre class="brush: xml; gutter: true"> &lt;?xml version=&quot;1.0&quot;?&gt;
 &lt;rdf:RDF xmlns:rdf=&quot;http://www.w3.org/1999/02/22-rdf-syntax-ns#&quot;
 xmlns:contact=&quot;http://www.w3.org/2000/10/swap/pim/contact#&quot;&gt;
 &lt;contact:Person rdf:about=&quot;http://www.w3.org/People/EM/contact#me&quot;&gt;
     &lt;contact:fullName&gt;Eric Miller&lt;/contact:fullName&gt;
     &lt;contact:mailbox rdf:resource=&quot;mailto:em@w3.org&quot;/&gt;
     &lt;contact:personalTitle&gt;Dr.&lt;/contact:personalTitle&gt; 
   &lt;/contact:Person&gt;
 &lt;/rdf:RDF&gt;</pre>

—**Web Ontology Language**，**OWL**

        OWL 与 RDF 有很多相似之处，但是较之 RDF， OWL 是一门具有更强机器解释能力的更强大的语言。

与 RDF 相比，OWL 拥有更大的词汇表以及更强大的语言。

        2003 年7 月W3C 公布了OWL Web ontology 语言的最初工作草案,2004 年2 月10 日,OWL 正式成为W3C 推荐的标准。OWL 和DAML + OIL 非常相近,只有一些微小的变化。DAML + OIL 和OWL 的语义都基于描述逻辑(descriptionlogic ,DL) 。OWL 作为W3C 推荐的标准本体表示语言,它的最大特点是关联描述逻辑, 通过对概念、概念属性及其相互间关系的描述,构成概念的复杂关系网络,这就意味着描述逻辑推理机可以推理OWL 本体。

        OWL 有3 个表达能力递增的子语言:OWL Lite ,OWL DL , OWL Full[20 ] 。OWL Lite 提供了类层次的能力和简单的约束能力,支持基数为0 或1 的基数约束,包括6 个类别的语言构造子。OWL DL 在保持计算完整性( computational completeness ) 和可判定性(decidability) 的前提下,提供了尽可能大的表达能力,包含了OWL 的全部语言构造成分,但他们的使用受到一些限制(如一个类可以是许多类的子类,但不能是另一个类的实例) 。描述逻辑是OWL 的形式化基础,OWL DL 的主要扩充是增加了布尔逻辑运算操作。OWL Full 包含OWL 的全部语言构造成分并取消了OWL DL 的限制,在OWL Full 中一个类可以看成个体的集合,也可以看成是一个个体。由于OWL Full 取消了OWL DL 中的保证可计算的某些限制,在没有计算保证的语法自由的RDF 上进行最大程度表达, 允许一个Ontology 在预定义的(RDF、OWL) 词汇表上增加词汇,从而任何推理软件均不能支持OWL FULL 的所有特点,因此不存在完整的推理算法支持OWL Full 的全部特性。OWL 通过对概念、概念属性及其相互间关系的描述,构成概念的复杂关系网络。
OWL本体的一个优点是会有能够对其做推理的工具。这些工具提供了不特定于某个主题领域的通用支持，而如果要构建一个能对一个特定的工业界标准XML Schema做推理的系统，它往往是特定于一个领域的。构建一个可靠的和有用的推理系统不是一项简单的工作。而创建一个本体则更为容易处理。

        OWL旨在提供一种可用于描述网络文档和应用之中所固有的那些类及其之间关系的语言。OWL网络本体语言当前已经获得万维网联盟认可的，用于编纂本体的知识表达语言家族。 其功能在于为网络文档和应用中固有的类以及其间的逻辑关系提供描述，使得基于此技术的网络应用更加 人性化和智能化，节省用户自身资源搜索时间并将这些处理交给计算机系统内部处理。基于不同的语义论特性 此家族语言大致分为两个系统： 基于描述逻辑进而丰富表达和精准计算属性的OWL DL和OWL Lite，以及以资源描述架构RDF提供兼容叙述的OWL Full。 网络本体语言已经被认为是语义网技术的基础语言并吸引了包括学术和商业范围内人士的广泛兴趣。

*   ##### **<span style="line-height: 28px;">本体相关工具介绍</span>**

       ——Jena [Jena下载](http://jena.apache.org/download/ "Jena下载")

        jena是惠普公司的一个项目，jena为应用程序开发人员提供了一套java接口对本体进行操作。这样我们就可以调用jenaAPI，构建我们自己的应用程序，实现对包括RDF，OWL本体进行创建，修改，查询以及推理操作。主要包括：

a)       以RDF/XML、三元组形式读写RDF

资源描述框架是(RDF)是描述资源的一项标准(在技术上是W3C的推荐标准)，Jena文档中有一部分呢详细介绍了RDF和Jena RDF API，其内容包括对Jena RDF包的介绍、RDF模型的创建、读写、查询等操作，以及RDF容器等的讨论。

b)       RDFS，OWL，DAML+OIL等本体的操作

Jena框架包含一个本体子系统（Ontology Subsystem），它提供的API允许处理基于RDF的本体数据，也就是说，它支持OWL，DAML+OIL和RDFS。本体API与推理子系统结合可以从特定本体中提取信息，Jena 2还提供文档管理器（OntDocumentManager）以支持对导入本体的文档管理。

c)       利用数据库保存数据

    Jena 2允许将数据存储到硬盘中，或者是OWL文件，或者是关系数据库中。本文处理的本体就是OWL文件读入的。

d)       查询模型

Jena 2提供了ARQ查询引擎，它实现SPARQL查询语言和RDQL，从而支持对模型的查询。另外，查询引擎与关系数据库相关联，这使得查询存储在关系数据库中的本体时能够达到更高的效率。

e)       基于规则的推理

        Jena 2支持基于规则的简单推理，其推理机制支持将推理器(inference reasoners)导入Jena，创建模型时将推理器与模型关联以实现推理。

        Jena提供的接口本质上都是Java程序，也就是.java文件经过javac之后生成的.class文件。显然，class文件并不能提示本体创建使用的语言。为了区别于其他的表示方法，每种本体语言都有一个自己的框架（profile），它列出了这种语言使用的类（概念）和属性的构建方式和URI。因此，在DAML框架里，对象属性（）的URI是daml:ObjectProperty，而在OWL框架里却是owl:ObjectProperty。RDFS并没有定义对象属性，所以在RDFS框架里，对象属性的URI是null。
在Jena中，这种框架通过参数的设置在创建时与本体模型（Ontology Model）绑定在一起。本体模型继承自Jena中的Model类。Model允许访问RDF数据集合中的陈述（Statements），OntModel对此进行了扩展，以便支持本体中的各种数据对象：类（classes）、属性（properties）、实例（个体individuals）。

 ——Protege [download protégé software](http://protege.stanford.edu/download/download.html "download protégé software")

Protégé是一个开源的本体编辑器（目前的版本是Protégé4.3），用户可以在GUI环境下创建本体或者知识库。

——SparQL

        SparQL(Simple Protocol and RDF Query Language)，是为RDF开发的一种查询语言和数据获取协议，它是为W3C所开发的RDF数据模型所定义，但是可以用于任何可以用RDF来表示的信息资源。
SparQL 协议和 RDF 查询语言（SparQL）于2008年1月15日正式成为一项W3C推荐标准。SparQL 构建在以前的 RDF 查询语言（例如 rdfDB、RDQL 和 SeRQL）之上，拥有一些有价值的新特性。
而且，SparQ将Web2.0和Semantic web两种新的web技术联系起来了，很有可能成为将来的主流网络数据库的查询语言和数据获取标准。

*   ##### **参考文献**

[Web 3.0时代：网络对你无所不知](http://www.china.com.cn/economic/txt/2011-03/01/content_22025450_2.htm "Web 3.0时代：网络对你无所不知")
[本体（Ontology）综述](http://imarine.blog.163.com/blog/static/51380183200861373316920/ "本体（Ontology）综述")
[RDF 简介](http://www.w3school.com.cn/rdf/rdf_intro.asp "RDF 简介")
[RDF入门 推荐标准](http://www.360doc.com/content/05/1104/11/677_27683.shtml "RDF入门 推荐标准")
[OWL 简介](http://www.w3school.com.cn/rdf/rdf_owl.asp "OWL 简介")
[Jena 简介](http://www.ibm.com/developerworks/cn/java/j-jena/ "Jena 简介")
[实用语义网RDFS与OWL高效建模(英文版)](http://www.amazon.cn/gp/product/B001P5HR2I/ref=as_li_qf_sp_asin_tl?ie=UTF8&amp;camp=536&amp;creative=3200&amp;creativeASIN=B001P5HR2I&amp;linkCode=as2&amp;tag=ovjaywang-23)![](http://ir-cn.amazon-adsystem.com/e/ir?t=ovjaywang-23&amp;l=as2&amp;o=28&amp;a=B001P5HR2I)
[数据库支持的模糊OWL本体管理](http://www.amazon.cn/gp/product/B005CLOYGS/ref=as_li_qf_sp_asin_tl?ie=UTF8&amp;camp=536&amp;creative=3200&amp;creativeASIN=B005CLOYGS&amp;linkCode=as2&amp;tag=ovjaywang-23)![](http://ir-cn.amazon-adsystem.com/e/ir?t=ovjaywang-23&amp;l=as2&amp;o=28&amp;a=B005CLOYGS)
[语义Web原理及应用](http://www.amazon.cn/gp/product/B002NKMS7S/ref=as_li_qf_sp_asin_tl?ie=UTF8&amp;camp=536&amp;creative=3200&amp;creativeASIN=B002NKMS7S&amp;linkCode=as2&amp;tag=ovjaywang-23)![](http://ir-cn.amazon-adsystem.com/e/ir?t=ovjaywang-23&amp;l=as2&amp;o=28&amp;a=B002NKMS7S)
<script type="text/javascript" src="http://wms-cn.amazon-adsystem.com/20070822/CN/js/link-enhancer-common.js?tag=ovjaywang-23">// <![CDATA[

// ]]></script>

<noscript>
    ![](http://wms-cn.amazon-adsystem.com/20070822/CN/img/noscript.gif?tag=ovjaywang-23)
</noscript>