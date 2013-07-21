
<head>
<meta http-equiv="Content-Type" content="text/html;charset=gbk"/>
<meta name="title" content="GitParable"/>
<meta name="generator" content="Org-mode"/>
<meta name="generated" content="2012-11-02 21:03:28 中国标准时间"/>
<meta name="description" content="翻译The Git Parable，一篇关于Git的比喻"/>
<meta name="keywords" content="Git,Github,版本控制系统,版本控制,CVS,VCS"/>
<style type="text/css">

</style>
<script type="text/javascript">
<!--/*--><![CDATA[/*><!--*/
 function CodeHighlightOn(elem, id)
 {
   var target = document.getElementById(id);
   if(null != target) {
     elem.cacheClassElem = elem.className;
     elem.cacheClassTarget = target.className;
     target.className = "code-highlighted";
     elem.className   = "code-highlighted";
   }
 }
 function CodeHighlightOff(elem, id)
 {
   var target = document.getElementById(id);
   if(elem.cacheClassElem)
     elem.className = elem.cacheClassElem;
   if(elem.cacheClassTarget)
     target.className = elem.cacheClassTarget;
 }
/*]]>*///-->
</script>

</head>
<body>

<div id="preamble">

</div>

<div id="content">
<h1 class="title">The Git Parable：Git传说</h1>
<h2 style="color: #6d6d6d; font-size:18px; text-align: center; margin-left: 20em;">-------- 毛球子好为人师</h2>


<div id="table-of-contents">
<h2>目录</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 译者的话</a></li>
<li><a href="#sec-2">2 前言</a></li>
<li><a href="#sec-3">3 比喻(Parable)</a>
<ul>
<li><a href="#sec-3-1">3.1 快照(Snap）</a></li>
<li><a href="#sec-3-2">3.2 分支（Branches）</a></li>
<li><a href="#sec-3-3">3.3 分支名称（Branch Names）</a></li>
<li><a href="#sec-3-4">3.4 标签（Tags）</a></li>
<li><a href="#sec-3-5">3.5 分发（Distributed）</a></li>
<li><a href="#sec-3-6">3.6 离线（Offline）</a></li>
<li><a href="#sec-3-7">3.7 合并（Merges）</a></li>
<li><a href="#sec-3-8">3.8 重写历史记录(Rewirting History)</a></li>
<li><a href="#sec-3-9">3.9 “缓冲”区（Staging Area）</a></li>
<li><a href="#sec-3-10">3.10 找差异（Diffs）</a></li>
<li><a href="#sec-3-11">3.11 消除重复（Eliminating Duplication）</a></li>
<li><a href="#sec-3-12">3.12 压缩文件（Compressing Blobs）</a></li>
</ul>
</li>
<li><a href="#sec-4">4 真正的Git（The True Git）</a></li>
<li><a href="#sec-5">5 资源</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> 译者的话</h2>
<div class="outline-text-2" id="text-1">

<p> 一直以来都觉得CVS等版本控制系统很神秘，自己也想使用。也跟着在Github网站上的教程做过一次，但是始终不得要领。正好看到这样<a target="_blank" href="http://tom.preston-werner.com/2009/05/19/the-git-parable.html">一篇文章</a>。
本人水平有限，并且翻译的时候喜欢添油加醋，罗哩罗嗦，还爱加上自己有限的理解和调侃，自娱自乐，还请不喜欢我风格的人轻点儿拍砖。
</p>
</div>

</div>

<div id="outline-container-2" class="outline-2">
<h2 id="sec-2"><span class="section-number-2">2</span> 前言</h2>
<div class="outline-text-2" id="text-2">

  <p>Git，它其实是一个非常简单却又非常非常给力的系统。我们先来看看在大多数情况下，高手们是怎么教一个新手学习Git的呢？一般来说，高手一上来，会先给我们示范一堆乱七八糟的命令。然后，然后？没有然后了，教完了！而且末了还不忘加上一句：你看！就是这么滴简单～啧啧啧，我觉得这种方式很不妥：照这么个教法儿，很有可能，我们会学会用Git的来做几个简单的小任务，但是，我估计，你肯定会觉得Git很神奇，很魔幻，很科幻，很武侠……而且，想用这些神奇的特性做任何高级一点儿的东西都会很困难。所以，想真正使用Git的话，这么教（或者这么学）可不成，你得理解Git的一些基本概念。</p>
<p>下面，我会用一个Parable（比喻），从最最基本的概念起模拟Git是怎么一步一步衍生出来的。理解这些概念非常重要，理解他们以后，你就算是准备好怎么榨干Git身上的每一滴血了！（邪恶）其实概念们本身很简单，但是简单的概念组合起来之后，就能干一大堆很神奇的事儿了。你把我这篇文章读完了，就好比打通了任督二脉，任何歪门邪道的功夫一练就会，一会就精；同理，任何乱七八糟的Git的命令拿来就用，用了就好使！
</p>
</div>

</div>

<div id="outline-container-3" class="outline-2">
<h2 id="sec-3"><span class="section-number-2">3</span> 比喻(Parable)</h2>
<div class="outline-text-2" id="text-3">

<p>从现在开始，假设你有个破电脑，上面就一个文本编辑器，再加上几个控制文件的命令。然后，你做了个重要的决定，你决定就用这个电脑这个系统写一个大型软件项目。你需要个方法来管理软件的版本，以后想要看看之前某个版本的时候，或者想恢复过去的时候能够找到它。于是你满世界去找这种方法，但是没找到……因为您是一位非常负责任的开发者，你一赌气，干脆自己发明一个吧！接下来，我们的故事就是：你到底可能怎么发明这么一个“版本控制系统”（VCS），还有你当时是怎么寻思的！
</p>

</div>

<div id="outline-container-3-1" class="outline-3">
<h3 id="sec-3-1"><span class="section-number-3">3.1</span> 快照(Snap）</h3>
<div class="outline-text-3" id="text-3-1">

  <p>阿福是你的好朋友，他在影楼工作，专门给别人拍摄一些“特殊瞬间”（额……就是特别珍贵的瞬间）。实际上，他的工作就是见天儿地给一些瞎摆pose的天真可爱的小屁孩儿照相。一次，你俩又习惯性的一起吃饭，阿福给你八卦了些他工作上碰到的趣事儿：有位妈妈，每年都会在同一天，带他的女儿过来照一张肖像。她说她想要记下她宝贝女儿每个阶段的样子，就好象这些照片儿真的能带她穿越回去一样。</p>
<p>正所谓“有心什么什么什么不什么，无心插柳柳成荫”，阿福的一句话，你也穿越了，穿越了横亘在你面前的一道难关。你想到了怎么来控制你的版本。对，就是所谓的“快照”，就像游戏中的存档一样，你真正关心和需要的的就是怎么能在各个不同的阶段把代码存个档，等到以后想要用的时候再能把它读出来。
  说书的一张嘴不能说两家话，不管阿福了。你开始编程，建立了一个工作目录working。编程的时候，一次添加一个功能，每编好一个功能，就把整个工作目录working复制一份，起个名儿叫快照0（snapshot-0）。然后对灯发誓，保证永远不会改变这个目录里的任何东西。然后继续工作，又完成了一个功能，于是又复制了一遍工作目录working，这次起名儿叫快照1（snapshot-1）。</p>
<p>为了方便以后记起你对每一份快照都做过什么改变，你在每一个快照（就是复制的整个目录）下增加一个文件，起个名儿叫信息（message），专门在里面写一份总结陈词，老实交待在何年何月何日对这个快照做过什么。以后忘了或者不小心改错了哪些东西，就会来看看，有需要的东西就复制走。
</p>
</div>

</div>

<div id="outline-container-3-2" class="outline-3">
<h3 id="sec-3-2"><span class="section-number-3">3.2</span> 分支（Branches）</h3>
<div class="outline-text-3" id="text-3-2">

<p>经过努力的工作，你觉得项目差不多成型了，马上可以发表了。这时候可能已经到了快照99（snapshot-99，就是即将发布的1.0正式版）。终于你发布了这1.0版本给我们这些翘首以盼着的围观群众们。然后，你被我们异常激烈的反响感动坏了，毅然决定继续下去，开始开发威力加强版。
到现在为止，你的"版本控制系统"（VCS）非常成功，所有旧的版本都静静的呆在那里，你需要的时候可以轻易地找到。没过多久，大家开始反馈1.0版本的bug，这时候你很高兴地看到，你已经保留了所有版本的副本，所以你可以再把快照99（snapshot-99）拿出来修改bug。
  然而，自从上次发布之后，你继续开发的威力加强版也已经有了10个快照了，这10个快照显然跟你要修改bug的版本，也就是新的1.01版不同。所以，你只能把之前的快照99拿出来，放到工作目录（working）中，添加几行代码来解决掉那些小bug。</p>
<p>这时，你发现了一个问题。尽管你的版本控制系统对之前的“直线型开发”很有效，但是现在你改好bug的版本并不直接是上一个版本的后续版本，换句话说，改好的这个版本的真正父版本是快照99（snapshot99），而现在你却已经又有了10个快照。如果把改好bug的版本命名为快照110（snapshot-110）的话，之前“直线型结构”就会被破坏，以后也没有什么办法来判断这个快照的父快照究竟是谁。很显然，你现在需要一个，比之前“直线型结构”更给力的结构，来控制你的版本。</p>
<p>有研究表明，有时候，哪怕很短的一段时间，去接触一下大自然，能够显著地改善你的创造力。你已经在显示器旁努力工作了好几天了，说不定，在弥漫着初秋的芬芳的树林中漫步一下，会给你带来好运，帮助你想出一个好点子。</p>
<p>田野里，一排排长长的橡树路，永远是那么的迷人。它们孤伶伶地伫立在那儿，给人的感觉像要跟头顶上湛蓝的天空对抗什么似的。红宝石色的树叶散落一地，树枝看上去光秃秃的，错综盘杂。你的目光慢慢的定在了其中的一个树枝上，漫无目的地想看出怎么沿着它找回树干。大自然鬼斧神工打造的这个天然的枝杈的结构是多么复杂，但是你想要沿着某条树梢回到树干却毫不费力！这不正好解决了跟踪多条线开发出的程序的问题么！这也证明了他们“接触自然，点子自来”的研究成果是正确的。
重新审视你代码的各个版本，这次将他们想象成一棵树，之前遇到的问题迎刃而解。你只要把每个快照（snapshot）的父快照的”指针“记录在信息（message）文件中保存下来，就可以很轻易地沿着各个”指针“找回去了。
</p>
</div>

</div>

<div id="outline-container-3-3" class="outline-3">
<h3 id="sec-3-3"><span class="section-number-3">3.3</span> 分支名称（Branch Names）</h3>
<div class="outline-text-3" id="text-3-3">

  <p>现在，你所有代码的存档看上去就像棵树一样，而且现在你有了两个最新的快照，每一个分支一个快照。但是之前你可以很轻易地根据快照名称来确定哪个是最新的快照，现在却不行了。</p>
  <p>又因为现在将代码分支非常简单，所以你会希望以后一直这么用它：改bug创建个分支、试验新功能创建个分支等，实际上，从此以后，几乎每一个新的想法你都会想要新建一个分支出来！</p>
  <p>不过嘛，有利就有弊。每一次你新创建出一个快照，不管是哪一个分支下面的，你必须把它作为它那一个分支最新的快照记下来。要不然每次想要换到另外一个分支去工作会十分头疼。</p>
  <p>每一次分支的时候，你可能会在心里给这个分支一个名称，比如这个是1.0版本bug维护专用。之前威力加强版那个分支，你可能会叫它主分支（master）。</p>
  <p>再多想一想，就把代码的历史版本们看成一棵树，给每个树枝命名有什么用处？每一个分支都命名会占用大量的空间，而且并不能有效率地帮助确定哪个快照是这个分支最新的快照。</p>
  <p>想要定位一个分支，最有效的办法就是找到它最新的那个快照，然后沿着快照找回去就能得到整个儿分支历史了。</p>
  <p>存储分支的名称很简单,建立一个叫branches的文件，里面列出每个分支的最新的快照版本（因为它代表了这个分支）和分支相对应的名称。想要切换到某一个分支，只需要查看这个文件，找出该分支最新的快照即可。</p>
<p>由于你只存储了每一个分支最新的快照，所以每次增加快照的时候，也得改这个存储着快照版本和分支名称的branches文件，就是做更新。从而确保branches文件能同步反映你版本历史的结构。这也算一个小小的额外的负担吧。
</p>
</div>

</div>

<div id="outline-container-3-4" class="outline-3">
<h3 id="sec-3-4"><span class="section-number-3">3.4</span> 标签（Tags）</h3>
<div class="outline-text-3" id="text-3-4">

<p>在使用了分支（Branches)一段时间之后，你发现分支还有一些其它的好处，它可以有这么两种形式：
</p><ol>
<li>它就像一个可以删除的”指针“一样，指向某些快照，从而能帮助你跟踪每个分支；
</li>
<li>它也可以作为指向某些快照的”指针“永久保存下来。
</li>
</ol>

<p>第一个功能使他可以用来跟踪开发进程，比如“bug修复维护版本”；第二个功能可以用来标记某些非常重要的快照，比如1.0版本，1.1版本。</p>
<p>如果继续将这两个功能放在同一个文件夹下，可能就会乱套了：两种形式都像个”指针“一样，但是一种可以删除，一种不能删除。为了使它更简洁，更优雅，你决定建立另外一个文件叫tags（标签），专门记录第二种名称。</p>
<p>这样，将两种”指针“分开记录，能帮助你避免不小心混淆删错。
</p>
</div>

</div>

<div id="outline-container-3-5" class="outline-3">
<h3 id="sec-3-5"><span class="section-number-3">3.5</span> 分发（Distributed）</h3>
<div class="outline-text-3" id="text-3-5">

  <p>自己工作太孤独了！要是能找个志同道合的朋友一起做这个项目该多好？不过你很幸运，你的朋友阿作，有一台跟你差不多的电脑，非常乐意帮你做这个项目。你呢，自然不会独享你创造出来的这个非常好的版本控制系统（VCS），所以你把它传授给了阿作，把你们项目的所有快照（Snapshot）、分支（Branches）和标签(Tags)也都传给了她，这样她就能体会到版本历史的好处了。</p>
  <p>阿作加入进来对项目来说非常好。但是她是个很会生活的人，她经常到一些偏远的地方进行长途旅行，通常那些地方都没有网络。她刚拿到这个项目的源代码，就飞去巴塔哥尼亚去了，将近一周左右你都联系不上她。不过这一周里你俩都没闲着，都编了很多代码。所以一周之后当她回来的时候，你们立马发现了你这个版本控制系统有很大的缺陷：你俩用的是一样的编码方式，所以都有了快照114，快照115(snapshot-115)，但你的快照114跟她的快照114完全不同。</p>
<p>更糟糕的是，因为名字一样，你们也没办法知道哪个快照是谁改过的了。所以你俩一块儿想出了个办法：
</p><ul>
<li>首先，以后快照的信息里（snapshot message）要包括作者的姓名和电子邮件；
</li>
<li>然后，快照名称不再用简单的数字命名，而是使用信息（message）文件生成一个hash。由于每一个信息文件（message）的时间、内容、父快照还有作者都是不同的，所以能够保证这些hash值各不相同。
</li>
</ul>

  <p>为了统一标准，你俩都同意用SHA1算法来生成40位的16进制的字串。你俩都用这种新的技术（方式）更新了各自代码快照历史。现在，你们两个的代码中不存在两个快照114目录这种冲突了，而是有了两个不同的快照目录：‘8ba3441b6b89cad23387ee875f2ae55069291f4b’ 和 ‘db9ecb5b5a6294a8733503ab57577db96ff2249e’。</p>
  <p>用这种新的方案（技术），把阿作的所有新快照都复制到你的电脑上就很简单了。因为每一个快照都自动指向它的父快照，而完全相同的信息（message)，也就是相当于完全相同的快照，不论是在哪里建立的，就会有完全相同的名字。复制好以后，整个代码历史还是能画成一棵树的样子，只不过现在的树由你和阿作两个人的快照组成。</p>
<p>有一点非常重要，所以还要再申明一遍。每个快照都通过一个它特有的SHA1值来“验明身份”（identify），它定位到父快照靠的也是父快照独特的SHA1值。所以，这些快照可以任意复制到任何地方，任何别的电脑上。而且不论在哪儿，都不丢失它原来的特性，就是你总能通过这个独特的SHA1“验证它的身份”并且确定它在项目历史记录中确切的位置。
</p>
</div>

</div>

<div id="outline-container-3-6" class="outline-3">
<h3 id="sec-3-6"><span class="section-number-3">3.6</span> 离线（Offline）</h3>
<div class="outline-text-3" id="text-3-6">

  <p>阿作喜欢旅行，所以他经常在飞机上或者在船上，而且她去的地方一般也没有网络。所以她大部分时间都是离线的。</p>
<p>所以，你也并不惊讶于，阿作非常赞美你的版本控制系统（VCS）。用它，所有日常的操作都可以在线下进行，只有她想要把快照发给你的时候才需要用到网络。
</p>
</div>

</div>

<div id="outline-container-3-7" class="outline-3">
<h3 id="sec-3-7"><span class="section-number-3">3.7</span> 合并（Merges）</h3>
<div class="outline-text-3" id="text-3-7">

  <p>在阿作再次出发去旅行之前，你安排她完善一个叫“math”的分支，在这个分支里实现一个函数来生成质数。与此同时，你也在完善“math”分支，你要实现另一个函数来生成魔法数（magic number）。过了一段时间之后，阿作回来了。现在你俩需要把这两个不一样的“math”分支合并成一个快照。因为你们俩做的是不同的功能，合并挺简单。但是创建快照的信息（message）文件时，你发现这个快照很特殊，它有两个父快照：一个是你的math分支中最新的快照，一个是阿作的math分支中最新的快照（注：还记得分支是怎么存储的吗？就是在所有快照文件的外面建立一个叫branches的文件，里面列出所有分支的名称和分支里最后一个快照的名称）。合并后的快照只包含合并这两个快照所必须做出的改变，而不包含额外的改变。（注：比如两个父快照有一个命名冲突，合并后的快照除了解决这个冲突更改了名称之外不包含任何其他的改动。我推测这样是为了容易管理）</p>
<p>现在合并好了，阿作把你有而她没有的那些快照复制过去，现在你们两个的历史记录完全一样了！
</p>
</div>

</div>

<div id="outline-container-3-8" class="outline-3">
<h3 id="sec-3-8"><span class="section-number-3">3.8</span> 重写历史记录(Rewirting History)</h3>
<div class="outline-text-3" id="text-3-8">

  <p>就像所有的开发者一样，你也有一种强迫症，希望代码能够保持整洁，并且组织得又合理，。因而你同样想要使你的代码的历史记录保持整洁。但是昨天晚上，你在酒馆儿喝高了，回家又开始写代码，还写了不少，一共写了好几个快照。结果今天早上，当你你回头看昨天晚上写的那写代码时，鸡皮疙瘩掉了一地：代码大体上还是好的，但是中间有很多错误，所以你又建了几个快照来更正那些错误。</p>
  <p>我们来假设你喝高了的时候开发的部分属于'drunk'（喝高了）分支,你从酒馆儿回来后一共完成了三个快照，我们先约定这样标记它们：'drunk'肯定指向的是这个分支的最新的快照，'drunk^'代表'drunk'的直接父快照，'drunk^^'则代表它的“爷爷”快照（父快照的父快照），'undrunk'代表“太爷爷”快照，是喝酒之前的最后一个快照。所以实际上，按照继承的顺序来排列，四个快照应该是：'undrunk','drunk^^','drunk^','drunk'。
  你非常想把这三个非常糟糕的快照整合成两个“结构合理”的快照：一个快照改动‘undrunk’里原来就有的一个函数，另一个快照给'undrunk'新增加了一个文件。为了实现你这个修订，你把'drunk'快照复制到工作目录（working），先删除掉新增加的那个文件，这样工作目录里就是刚刚改好函数的样子。然后你在信息（message）里面写上适当的内容，生成一个新的快照；在信息（message）文件里，这个快照的父快照你指定为'undrunk'的SHA1。实际上就相当于你从'undrunk'快照有分一个分支出来。现在，你再把'drunk'快照复制到工作目录来（这次什么东不删了），直接再创建一个新快照，指定它的父快照为刚才创建的那个新快照。</p>
  <p>最后一步，你把'drunk'这个分支名字指向刚才最后创建的那个快照。
现在，'drunk'分支里面包含的就是一个比你昨天晚上喝高了做的那些快照更“清新”的版本了。那些一团糟的快照已经没有什么用处了，你可以删掉它们或者就那么放着。没有分支名指向他们，所以以后你也很难再找到它们。不过只要你不删除它们，它们就一直在那儿。
</p>
</div>

</div>

<div id="outline-container-3-9" class="outline-3">
<h3 id="sec-3-9"><span class="section-number-3">3.9</span> “缓冲”区（Staging Area）</h3>
<div class="outline-text-3" id="text-3-9">

  <p>尽管你一直试着每次只专注于开发一个特性，有些时候难免分心，去做些完全无关的工作。而且常常都做到一半了，才发现工作目录（working）应该分成两个快照保存，因为现在已经有两个不同的特性了。
  为了帮你自己离开这尴尬的处境，“缓冲目录”的概念会很有用。这个区域基本上就是个中转站，中转你的工作目录和最终的快照。每次你完成一个快照，你也复制一份到缓冲（staging）目录里。现在，每次编辑好一个新文件、新建一个新文件、或者删除一个文件，你可以决定这些改变是否应该反映在下一个快照中。如果应该反映出来，你就先在缓冲区（staging）中模拟出来；如果不该反映出来，你可以就将它们先放在工作目录里，之后再反映到更新的版本中去。从现在开始，快照是通过缓冲目录来直接创建的了。</p>
  <p>这样把“编码工作”和“准备缓冲”给分开，你就可以更容易的指定哪些改变应该被包括在下一个快照中了。你再也不用担心编码的途中分心去做一些可能无关的改动了。</p>
  <p>不过，你也得小心一点儿。比如，假设有一个“自述文件“（README），你先编辑了一次，然后提交<sup><a class="footref" name="fnr.1" href="#fn.1">1</a></sup>到缓冲区（staging）里，然后继续编辑其他文件。过了一会儿，你又改动了这个自述文件（README）。现在你已经改动了自述文件两次，但是缓冲区只反映出一次改动！如果你这个时候创建快照的话，第二次改动不会反映出来。
这个故事告诉我们一个道理：每次编辑之后，如果想把编辑的内容包含到下一个快照中，一定要把它先提交到缓冲区（staging）里。
</p>
</div>

</div>

<div id="outline-container-3-10" class="outline-3">
<h3 id="sec-3-10"><span class="section-number-3">3.10</span> 找差异（Diffs）</h3>
<div class="outline-text-3" id="text-3-10">

  <p>你有一个工作目录（working directory）， 一个缓冲区（staging area），还有一群快照：对着这么一堆不同的目录，你怎么能知道哪两个目录之间都做了些啥变化？看快照的信息文件（message）吗？在信息文件中只能得到一个概括，而不是到底哪几行改过。</p>
  <p>用”找茬“算法（diffing algorithm），你可以写一个小程序来显示两个目录间的不同。因为当你把东西提交到缓冲区，一定想看一看跟工作目录比起来哪儿变了，从而决定是否还要提交些什么别的东西。看看缓冲和最近的快照之间的不同也很重要，因为这些差异是将来生成的快照和上一个快照之间差异的一部分。</p>
<p>你可能还想看看其他一些差异。比如，从某个特定的快照与它父快照之间的差异中，你能得到一个“改动集合”（changeset）；再比如看两个分支之间的差异会帮助你确保你的开发不会偏出主线太远。
</p>


</div>

</div>

<div id="outline-container-3-11" class="outline-3">
<h3 id="sec-3-11"><span class="section-number-3">3.11</span> 消除重复（Eliminating Duplication）</h3>
<div class="outline-text-3" id="text-3-11">

  <p>阿作溜达了几个月，去了纳米比亚，伊斯坦布尔，还有加拉帕戈斯，她开始抱怨你这个版本控制系统让她的电脑里充满了好几百份快照，而且它们都几乎差不多。你也觉得那么多份副本有点儿太占地儿。你想了想，居然让你又想出一个天才的点子。</p>
  <p>你想起来SHA1哈希算法能够对每一个文件生成一段特殊的字符串。于是你从最老的一个快照开始，转化你的代码历史：
</p><ul>
<li>首先，你在所有历史记录目录之外建立一个新目录，叫“组件”（objects）目录；
</li>
<li>然后，打开最老的那个快照中最深的目录
</li>
<li>接着，你打开一个临时文件（temp file），用来记录
</li>
<li>对这个目录下的每一个文件，做这么三件步骤：
<ol>
<li>计算这个快照的SHA1；
</li>
<li>在临时文件上记下一条，内容要包括：'blob'<sup><a class="footref" name="fnr.2" href="#fn.2">2</a></sup>这个单词、刚计算出来的SHA1、这个文件自己的名称；
</li>
<li>把这个文件改个名儿，新名字就用刚计算出来的SHA1值，然后复制到组件（objects）目录。
</li>
</ol>

</li>
<li>一旦完成了上面三个步骤，计算这个临时文件（temp file）的SHA1，然后把它也放在组件（objects）目录中（译者注：这个临时文件就是它所在的目录的“目录文件”）。
</li>
<li>如果某次复制到组件（objects）目录时，发现目录中已经有同名文件了，说明你已经有了一份这个文件了，不必再复制过来。
</li>
<li>现在，在目录中向上一层，再执行一遍上述步骤，只不过这一次，当碰到目录的时候，要向临时文件（temp file）里写这三块儿内容：“tree”这个单词+上次那个临时文件的SHA1值+目录名称（directory's name）。这么记录，你能建立了起一个"目录文件"<sup><a class="footref" name="fnr.3" href="#fn.3">3</a></sup>的树形结构，每个目录文件记录了它所包含的文件及其SHA1值，还记录了它所包含的其他目录文件及其SHA1值。
</li>
</ul>

  <p>一旦对这个快照的所有目录做完了上述转化，你就有了一个独特的“根目录文件”（root）。这个根目录文件没有父目路，所以你必须把它的SHA1记录在什么地方。最理想的方式就是把它记录在快照的信息（message）文件中。这么一来，这个快照的信息文件（message）它的SHA1值的独特性又通过增加了整个快照本身得到了增强<sup><a class="footref" name="fnr.4" href="#fn.4">4</a></sup>，你终于可以绝对保证两个拥有相同SHA1的信息文件的快照绝对是一样的！</p>
  <p>现在，同样方便的，你再用上述的方法对所有快照的信息文件进行转化。因为你一直都记录着你所有分支和标签的名称<sup><a class="footref" name="fnr.5" href="#fn.5">5</a></sup>，还有这些名称指向这些信息文件的SHA1值，所以你不担心会找不到任何重要的快照。</p>
  <p>由于在“组件”（object）目录里有了这些信息，你可以安全地把你用来产生这些信息的那个快照目录删除掉。之后如果你想再生成那样的完全的快照目录，只要沿着信息（message）文件中根目录文件（root）中的SHA1值一层一层找下去，并把它们指向的文件提取出来就好了。</p>
  <p>如果你只有一个快照，这个转化并不能节省多少空间。你相当于仅仅是把一个文件系统转化成了另外一个文件系统，而且还产生了一些额外的工作。但是这种转化真正带来的好处在于：如果你有很多个快照，这些快照里面有一些相同的文件或者说目录，它能够将这些文件和目录重用起来。想像一下：你有两个连续的快照，都有10个目录和100个文件，但是其中只有一个文件改动过。应用这种转化会为第一个快照生成10个目录文件（tree）和100个文件（blob）；但是为第二个快照仅生成1个文件（blob）和1个目录文件（tree）！</p>
  <p>通过把每一个快照目录从旧的系统转化成这个新的系统，你砍掉了一大堆重复的文件，显著地节约了空间。之前你可能存了50多个几乎差不多的文件副本，现在你只需要存一个了。
</p>
</div>

</div>

<div id="outline-container-3-12" class="outline-3">
<h3 id="sec-3-12"><span class="section-number-3">3.12</span> 压缩文件（Compressing Blobs）</h3>
<div class="outline-text-3" id="text-3-12">

<p>删除掉重复的文件和目录显著地节约了空间，但是你还可以做得更多。源文件都是文本文件，而用一些压缩算法，比如LZW或者DEFLATE能够极有效地压缩文本文件。如果你在计算SHA1之前先把所有文件压缩了，你又能节约一大部分项目历史记录所见的空间。
</p>
</div>
</div>

</div>

<div id="outline-container-4" class="outline-2">
<h2 id="sec-4"><span class="section-number-2">4</span> 真正的Git（The True Git）</h2>
<div class="outline-text-2" id="text-4">

  <p>到现在为止，你所建立的版本控制系统（VCS）跟原本的Git基本差不多了。最主要的区别可能在于Git提供了非常优雅的命令行工具来做上述那些事：创建新的快照，切换快照（Git中管快照叫commit），跟踪历史记录，保证分支是最新的，从别人那里抓去改动，合并分支，查看差异，还有另外几百条常用（或者不那么常用）任务。</p>
  <p>在你继续深入的学习Git的时候，记住这个“比喻”（parable）。Git从底层来看，它的想法是很简单的，不过这种简单又使它十分的灵活和强大。最后，在你去学习Git的命令之前，最后一件事是：记住在Git里，几乎不大可能丢失已经committed（生成快照）的工作。甚至你删除了一整个分支，所有的快照实际上仍然在“组件”（object）目录里，实际上你只是删除了指向最终快照的那个指针。要是真想找回那些快照，你需要知道它们的SHA值，可以翻一翻“git reflog”，那里记录着所有快照曾经都指向过哪里，万一有一天你真的不小心删错了东西，这东西简直能救命啊！
</p></div>

</div>

<div id="outline-container-5" class="outline-2">
<h2 id="sec-5"><span class="section-number-2">5</span> 资源</h2>
<div class="outline-text-2" id="text-5">


<p>
接下来是下一步你会用到的资源，去成为一名Git专家吧！
</p><ul>
<li><a href="http://learn.github.com/">Learn Git</a>
</li>
<li><a href="http://git-scm.com/book">Git Community Book</a>
</li>
<li><a href="http://www-cs-students.stanford.edu/~blynn/gitmagic/">Git Magic</a>
</li>
</ul>


<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">
<p class="footnote"><sup><a class="footnum" name="fn.1" href="#fnr.1">1</a></sup> 所谓的提交就相当于复制一份到缓冲区。
</p>


<p class="footnote"><sup><a class="footnum" name="fn.2" href="#fnr.2">2</a></sup> binary large object，可译作大型二进制目标文件。
</p>


<p class="footnote"><sup><a class="footnum" name="fn.3" href="#fnr.3">3</a></sup> 所谓的目录文件，就是之前保存好的临时文件。这么叫是因为它记录了他这个目录下的所有文件的SHA1值还有所有其他目录文件的SHA1值。
</p>


<p class="footnote"><sup><a class="footnum" name="fn.4" href="#fnr.4">4</a></sup> 还记得之前保证message文件的独特性是基于这样一个事实：每一个message都有独特的地址、独特的作者还有独特的附加信息，这个保证肯定不如将整个快照本身也加进来更强。
</p>


<p class="footnote"><sup><a class="footnum" name="fn.5" href="#fnr.5">5</a></sup> 还记得分支和标签节中你建立的<a href="#sec-3-3">branches</a>和<a href="#sec-3-4">tags</a>文件吗？
</p></div>
</div>

</div>
</div>
</div>

</body>
</html>
