**Title:** **Accelerating Dynamic Graph Analytics on GPUs**

**Author:** Zoi Kaoudi<sup>1</sup>  Jorge-Arnulfo Quiané-Ruiz<sup>1</sup> Saravanan Thirumuruganathan<sup>1</sup> Sanjay Chawla<sup>1</sup> Divy Agrawal<sup>2</sup>

**Affiliation:** <sup>1</sup>Qatar Computing Research Institute, HBKU <sup>2</sup>UC Santa Barbara*

**Publication Venue:** [SIGMOD '17](https://dl.acm.org/doi/proceedings/10.1145/3035918)

**Link:** https://dl.acm.org/doi/10.1145/3035918.3064042

**Summary[速读]:**

*[图文浏览。快速知道文章讲了什么：标题，摘要和引言。这篇论文是关于什么的？他解决了什么问题？迷人之处在哪？有什么新的东西（写文章的时候一定要强调文章中有什么新东西）？巧妙之处何在？]*

[引言。了解了这篇论文研究成果之后，接着问自己：我为什么要关注这个问题]

[摘要。将其分解并加上一些有趣的亮点，可能有利于阅读；把摘要翻译成中文]

由于图分析通常涉及计算密集型操作，因此GPU已被广泛用于加速处理。 然而，在诸如社交网络，网络安全和欺诈检测之类的许多应用中，它们的代表图经常发展，并且必须在GPU上执行图结构的重建以合并更新。 因此，重建图形成为处理高速图形流的瓶颈。 在本文中，我们提出了一种基于GPU的动态图存储方案，以轻松支持现有的图算法。 此外，我们提出了并行更新算法来支持有效的流更新，以便可以立即将维护的图形用于GPU上的高速分析处理。 我们在大型真实和合成数据集上使用三个流应用程序进行的广泛实验证明了我们提出的方法的优越性能。

**【精读】**

*[批判性阅读和创造性阅读。首先对论文进行否定质疑，仔细挑毛病；其次，对论文有了足够的了解之后，如果发现论文中提到的想法非常优秀，那么可以创造性地思考能用这篇论文做什么]*

[论文是否正确、真正地解决了问题？作者论文中所用方法是否有局限性？如果所读的论文没有解决问题，那么我能解决么？我能采用比论文中更简单的方法解决么？所以，一旦进入仔细阅读的状态，要在读论文之前对自己说：这篇论文可能有问题，我要找出来。这就是批判性阅读。]

[上半部分是比较客观的问题，包括论文的核心观点是什么？主要的局限性是什么？代码和数据是不是可得的？论文的贡献是否有意义？论文中的实验是否足够好？

图片的下半部分是比较主观的问题，包括我错过了什么相关论文么？这对我的工作有何帮助么？这是一篇值得关注的论文么？这个研究领域的领头人是谁呢？哪些公司、研究院、实验室值得关注？其他的人对这篇论文有何看法呢？如果有机会见到作者，我应该问作者什么问题？]

![image-20210409004446608](C:\Users\Chris\AppData\Roaming\Typora\typora-user-images\image-20210409004446608.png)



#### *What this paper is about*



Considering a common sliding window model on a graph edge stream, each element in the stream is an edge in a graph and analytic tasks are performed on the graph induced by all edges in the up-to-date window.

We thus propose two GPU-oriented algorithms, i.e. GPMA and GPMA+, to support e cient parallel batch updates.

The contributions of this paper are summarized as follows: We introduce a framework for GPU dynamic graph analytics and propose, the first of its kind, a GPU dynamic graph storage scheme to pave the way for real-time dynamic graph analytics on GPUs.



#### *What you can learn*



Connected Component Results: presents the results for running Connected   Component on the dynamic graphs.

GPMA and GPMA+ can also be extended to multiple GPUs to support graphs with a size larger than the device memory of one GPU.

Second, to avoid the rebuild of the graph structure which is a bottleneck for processing dynamic graphs on GPUs, we propose GPMA and GPMA+ to support incremental dynamic graph maintenance in parallel.

LASTZ :

Seeding ---> X-drop ungapped filtering ---> Extend

* Seed采用的是标准的方法。
* X-drop ungapped filtering即当分数低于max score -X 时候停止，如果max score大于阈值，就可以保留。
* Extend是标准的方法，对保留的序列进行扩展。



**【研读】**

*[尝试将文章中的算法实现一遍。除了阅读的方式，还要理解所读的论文是怎样写出来的。]*

[十个问题]

\1. 这篇文章究竟讲了什么问题？比方说你设计一个算法，它的 input 和 output 是什么？

\2. 这个问题的性质是什么？是一个新的问题吗？如果是一个新问题，它的重要性何在？如果不完全是一个新问题，那为什么它“仍然重要”？

\3. 这篇文章致力于证明什么假设？

\4. 有哪些与这篇文章相关的研究？这一领域有哪些关键人物？

\5. 这篇文章提出的问题解决方案中，核心贡献是什么？

\6. 实验是如何设计的？

\7. 实验是在什么样的数据集基础上运行的？

\8. 实验结果能否有力地支持假设？

\9. 这篇文章的贡献是什么？

\10. 下一步可以做什么？

Darwin-WGA:

Seeding(D-SOFT) ---> Gapped Flitering(Band Smith-Waterman) ---> Extend(GACT-X)

* D-SOFT参照Darwin
* Band Smith-Waterman参考经典的。
* GACT-X比起一般的GACT的区别有两点：
  * 引入了X-drop
  * 没有采用Smith-Waterman而是Needleman -Wunsh

最后实现了FPGA和ASIC。在敏感性上面，取得了很大的提升。在性能上面，和LASTZ比，FPGA慢一些，ASIC快一些；和iso-sensitive software（作者自己写的软件baseline）相比，快了很多。





@inproceedings{10.1145/3035918.3064042,
author = {Kaoudi, Zoi and Quiane-Ruiz, Jorge-Arnulfo and Thirumuruganathan, Saravanan and Chawla, Sanjay and Agrawal, Divy},
title = {A Cost-Based Optimizer for Gradient Descent Optimization},
year = {2017},
isbn = {9781450341974},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3035918.3064042},
doi = {10.1145/3035918.3064042},
abstract = {As the use of machine learning (ML) permeates into diverse application domains, there is an urgent need to support a declarative framework for ML. Ideally, a user will specify an ML task in a high-level and easy-to-use language and the framework will invoke the appropriate algorithms and system configurations to execute it. An important observation towards designing such a framework is that many ML tasks can be expressed as mathematical optimization problems, which take a specific form. Furthermore, these optimization problems can be efficiently solved using variations of the gradient descent (GD) algorithm. Thus, to decouple a user specification of an ML task from its execution, a key component is a GD optimizer. We propose a cost-based GD optimizer that selects the best GD plan for a given ML task. To build our optimizer, we introduce a set of abstract operators for expressing GD algorithms and propose a novel approach to estimate the number of iterations a GD algorithm requires to converge. Extensive experiments on real and synthetic datasets show that our optimizer not only chooses the best GD plan but also allows for optimizations that achieve orders of magnitude performance speed-up.},
booktitle = {Proceedings of the 2017 ACM International Conference on Management of Data},
pages = {977–992},
numpages = {16},
keywords = {optimization, data management systems, gradient descent, machine learning, big data},
location = {Chicago, Illinois, USA},
series = {SIGMOD '17}
}

Zoi Kaoudi, Jorge-Arnulfo Quiane-Ruiz, Saravanan Thirumuruganathan, Sanjay Chawla, and Divy Agrawal. 2017. A Cost-based Optimizer for Gradient Descent Optimization. In <i>Proceedings of the 2017 ACM International Conference on Management of Data</i> (<i>SIGMOD '17</i>). Association for Computing Machinery, New York, NY, USA, 977–992. DOI:https://doi.org/10.1145/3035918.3064042