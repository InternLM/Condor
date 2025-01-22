# Condor

[![arXiv](https://img.shields.io/badge/arXiv-2501.12273-b31b1b.svg)](https://arxiv.org/abs/2501.12273)
[![license](https://img.shields.io/github/license/InternLM/opencompass.svg)](./LICENSE)

## ✨ Introduction  

[[🤗 HuggingFace Models](https://huggingface.co/internlm/)]
[[🤗 HuggingFace Datasets](https://hf.co/datasets/internlm/Condor-SFT-20K)]
[[📃 Paper](./assets/CondorPaper.pdf)]
<!-- [[📃 Paper](https://arxiv.org/abs/)] -->
<!-- [[🧰 OpenXLab](https://openxlab.org.cn/models/detail/OpenLMLab/)] -->
<!-- [[🌐 Project Page](https://internlm.github.io/)] -->

> The quality of Supervised Fine-Tuning (SFT) data plays a critical role in enhancing the conversational capabilities of Large Language Models (LLMs).
> However, as LLMs become more advanced, 
> the availability of high-quality human-annotated SFT data has become a significant bottleneck, 
> necessitating a greater reliance on synthetic training data. 
> In this work, we introduce \textbf{Condor}, 
> a novel two-stage synthetic data generation framework that incorporates  \textbf{World Knowledge Tree} and \textbf{Self-Reflection Refinement} to produce high-quality SFT data at scale. 
> Our experimental results demonstrate that a base model fine-tuned on only 20K Condor-generated samples achieves superior performance compared to % RLHF-trained 
> counterparts. 
> The additional refinement stage in Condor further enables iterative self-improvement for LLMs at various scales (up to 72B), 
> validating the effectiveness of our approach. 
> Furthermore, our investigation into the scaling for synthetic data in post-training reveals substantial unexplored potential for performance improvements, 
> opening promising avenues for future research.

## 🦅 Condor

Condor is a two-stage data synthesis engine adopted in InternLM3, designed to generate high-quality data for supervised fine-tuning of large language models (LLMs). The human-preference performance of the model improves significantly when fine-tuned with Condor, without affecting the model's knowledge capacity. The Condor pipeline is divided into two stages: data synthesis and data refinement. 

- **Condor Void (Data Synthesis):**

  During the data synthesis stage, Condor introduces the \textbf{World Knowledge Tree}, which serves as a foundation of tags for data generation. Next, we apply task and difficulty expansion to enhance the diversity and complexity of questions under each tag, leading to the creation of the initial synthetic QA dataset.

- **Condor Refine (Data Refinement):**

  In the data refinement stage, Condor employs a \textbf{Self-Reflection Refinement} strategy, allowing the model to iteratively optimize the responses by generating new critiques and obtain the final refined dataset.

## 👨🏻‍💻 Prompt for Dataset Construction

**Prompt for Question Synthesis**

<details><summary>click to expand</summary>


```
Now we need to create high-quality SFT data for LLM training, so we need you to produce a batch of such data. You only
need to create Questions. I will give you a theme and some examples of SFT data Questions. You need to create three
Questions of different difficulty levels based on this new theme.\\
Your Questions must meet the following requirements:\\
1. You must strictly create only three Questions at a time. These three Questions must be in the domain of \textcolor{red}{[[domain]]}
and the Questions should align with the given theme of \textcolor{red}{[[theme]]}.\\
2. The Questions you create must have context and sufficient information; they should not be abrupt and directly ask the
question.\\
3. Your reply must strictly follow the format below. Your Questions need to be included between [Question Start] and
[Question End], and the difficulty level should be indicated at the beginning, as in the following format:\\

[Easy][Question Start]Question[Question End]

[Medium][Question Start]Question[Question End]

[Hard][Question Start]Question[Question End]

4. Your Questions of different difficulty levels should be distinct and actually reflect the different levels of difficulty.\\
\quad \\
Here are some examples of high-quality SFT data Questions for \textcolor{red}{[[domain]]}:
\textcolor{red}{[example list]}\\
Now it's your turn. Please provide the three Questions of different difficulty levels you created about the theme of
\textcolor{red}{[[theme]]} for \textcolor{red}{[[domain]]}, according to the requirements. Do not be confined by the theme; your Questions only need to
be related to the theme. You can use your rich imagination, but note that you cannot copy the expression from the
examples; you must have your own new expression:
```

</details>

<br>

**Prompt for Response Critic**

<details><summary>click to expand</summary>


```
There is now a user’s question and a model’s response. You need to write a critique for this response, pointing out the
strengths and weaknesses of the model’s answer to help the model improve its response.

Your critique must strictly adhere to the following format:

[Critique Start]

[Strength Start]Strength[Strength End]

[Weakness Start]Weakness[Weakness End]

[Suggestion Start]Suggestion[Suggestion End]

[Critique End]

That is, you must place the strength, weakness, and suggestion in their respective sections.

Here is the user’s question and the model’s response: \textcolor{red}{[dialogue]}

Now it’s your turn. Please provide your Critique as required:
```

</details>

<br>

## 🤗 Datasets and Model Zoo 

The datasets and models are available on Huggingface.

|        Dataset         |                       Huggingface Repo                       |
| :--------------------: | :----------------------------------------------------------: |
| Condor-SFT-20K(Refine) | [Dataset Link](https://hf.co/datasets/internlm/Condor-SFT-20K) |

<!-- |    Model    |                        Huggingface Repo                        |
| :---------: | :------------------------------------------------------------: |
| Condor-7B  | [Model Link](https://huggingface.co/internlm/)  |
| Condor-72B  | [Model Link](https://huggingface.co/internlm/)  | -->

## 📝 Examples

**Condor Refine Example - English**

<details><summary>click to expand</summary>


```
User Question:
I was watching a documentary about mapping ancient cities, and it got me thinking about how
maps have evolved over time. Have you ever seen an old map and marveled at how different it looks
from today's maps? What's the oldest map you've ever seen?
```

```
Origin Answer:

As a digital AI assistant, I don't have personal experiences, emotions, or visual interactions, so I
haven't "seen" maps in the classical sense. I don't have a physical presence, and my interactions
are limited to text-based conversations. However, I'd be delighted to take you on a journey
through the evolution of maps and highlight some notable examples of ancient and historic maps!

The Evolution of Maps
1. Prehistory (~20,000 BCE - 3,000 BCE):
Early maps were often simple, symbolic, and focused on specific areas, like the Turin Papyrus Map
(~1160 BCE), which depicts the location of gold mines in ancient Egypt.
2. Ancient Civilizations (~3,000 BCE - 500 CE):
- Babylonian Map of the World (~600 BCE): A clay tablet showing the world as a flat disk,
surrounded by an ocean.
- Ptolemy's World Map (~150 CE): A more accurate, yet still flawed, representation of the
known world, using longitude and latitude.
3. Medieval Period (~500 - 1500 CE):
- Mappa Mundi (~1300 CE): A symbolic, Christian-centric map, often displaying Jerusalem at the
center.
4. Age of Exploration (~1500 - 1700 CE):
- Waldseemüller Map (1507 CE): One of the earliest maps to depict the New World, naming
America after Amerigo Vespucci.
5. Modern Cartography (~1700 CE - present):
- Triangulation and Surveying: Led to more accurate mapping of territories.
- Aerial Photography and Satellite Imaging (20th century): Revolutionized mapmaking with high-
resolution, globally consistent data.
- Digital Maps (late 20th century - present): Enabled interactive, dynamically updated, and
highly accurate maps, like Google Maps.

Some of the Oldest Known Maps
- Cave of El Castillo Map (~14,000 BCE): A simple, prehistoric map etched into a cave wall in
Spain, showing the location of a nearby water source.
- The Bedolina Map (~5,000 BCE): A rock carving in Italy, depicting a valley with topographical
features.
- The Nubian Map (~2,000 BCE): An ancient Egyptian map, showing the location of Nubian gold
mines and territories.

Marveling at Old Maps
While I may not have personal experiences, I can certainly help you appreciate the historical
context, artistic value, and cartographic innovations of old maps. If you'd like to discuss a specific
map or era in more detail, feel free to ask!
Which aspect of old maps fascinates you the most? Is it:
•A) The artistic and symbolic representations
•B) The historical context and cultural influences
•C) The cartographic innovations and technological advancements
•D) Something else (please share!)
```

```
Reflection:
[Strength Start]
Strengths:
1.Comprehensive Response:
The model provides an exhaustive overview of the evolution of maps, covering various historical periods, notable examples, and technological
advancements.
2.Structured Formatting:
The use of clear headings, numbered lists, and concise bullet points enhances readability and facilitates easy understanding of complex
information.
3.Engagement Initiator:
The response ends with an interactive element, encouraging user participation and potentially leading to a more in-depth discussion.
4.Honesty About Limitations:
The model transparently acknowledges its limitations as a digital AI assistant, setting clear expectations for the user.
[Strength End]

[Weakness Start]
Weaknesses:
1.Length and Information Overload:
The response is lengthy and packed with numerous examples, which might overwhelm the user. Some points could be elaborated upon in
subsequent interactions rather than all at once.
2.Lack of Visual Enhancement:
Despite discussing maps, the response is text-only. Incorporating images, diagrams, or even suggesting external visual resources could
significantly enhance the user's understanding and engagement.
3.Initial Acknowledgement Could Be Brief:
While honesty about the model's limitations is appreciated, the initial acknowledgement could be more concise to quickly transition to the
more engaging and informative sections.
4.Question Response Mismatch:
The user inquired about the oldest map the model has "seen," which the model addresses by stating its inability to see. However, the model
could more directly address the implicit curiosity about old maps by initially highlighting one or two of the oldest known maps before delving
into the broader evolution.
[Weakness End]

[Suggestion Start]
Suggestions for Improvement:
1.Tiered Information Disclosure:
Initially provide a brief overview of the evolution of maps and highlight 2-3 of the oldest known maps. Offer the user the option to explore
specific eras or types of maps in more detail, facilitating a more interactive and paced information exchange.
2.Incorporate Visual Aids or References:
Suggest reputable online resources or include descriptions that encourage users to visually explore the mentioned maps, enhancing their
understanding of cartographic developments.
3.Refine the Initial Limitation Disclosure:
Condense the initial acknowledgement to a single sentence, swiftly moving the focus to the engaging content (e.g., "As a text-based AI, I'll
guide you through the fascinating evolution of maps, highlighting notable examples and innovations.").
[Suggestion End]
```

```
Refined Answer:

Discovering the Ancient Roots of Modern Maps

As a text-based AI, I'll guide you through the fascinating evolution of maps, highlighting notable examples and innovations.

Let's Start with the Oldest Known Maps:
1.Cave of El Castillo Map (~14,000 BCE):
Etched into a Spanish cave wall, this simple map shows the location of a nearby water source.
2.The Bedolina Map (~5,000 BCE):
A rock carving in Italy, depicting a valley with topographical features.
Visual Exploration Suggestion: Visit the British Museum's Online Collection or Google Arts & Culture to see high-resolution images of these
ancient maps.**

Curious About the Evolution of Maps?
Here's a concise overview. Feel free to pick any era to explore in more depth:
- Prehistory (~20,000 BCE - 3,000 BCE): Simple, symbolic maps (e.g., Turin Papyrus Map)
- Ancient Civilizations (~3,000 BCE - 500 CE): Notable examples include Babylonian Map of the World and Ptolemy's World Map
- Medieval to Modern (~500 - present): Advances from Mappa Mundi to Triangulation, Aerial Photography, and Digital Maps like Google
Maps

Which Era or Aspect of Old Maps Would You Like to Explore Further?
•A) Ancient symbolic representations
•B) Medieval navigational charts
•C) The leap to digital cartography
•D) Something specific (please share, and I'll delve deeper!)
```

</details>

<br>

**Condor Refine Example - Chinese**

<details><summary>click to expand</summary>


```
User Question:
你是一位来自古代的礼器，曾在重要的祭祀仪式中使用。请用第一人称叙述，你⻅证了哪些古代的重要节日和仪式，以及你在这
些活动中的⻆色和感受。
```

```
Origin Answer:
我，一件被精心雕琢的⻘铜礼器，自诞生之日起，便在中华古国的庄严祭坛上占有一席之地。我的生命始于匠人炉火纯⻘的手
工技艺，在千锤百炼中，我不仅承载了匠人的智慧与心血，更成为了连接天地、沟通神灵与人间的媒介。

在那些遥远的年代里，我⻅证了无数庄重而又壮观的祭祀仪式。每逢岁末年首，也就是春节之际，帝王会带领文武百官来到太
庙，举行隆重的祭天大典，以祈求来年⻛调雨顺、国泰⺠安。此时，我会被摆放在祭坛中央，盛满美酒，供献给上天，而我的身上，
也会覆盖着象征吉祥如意的红绸缎。那一刻，我能感受到所有人的目光都聚焦于我，仿佛通过我，人们的心愿便能直达天听。
而在春分秋分这样的重要节气，祭祀祖先的礼节同样不可少。人们相信，通过祭祀可以得到先灵的庇护，确保农作物的丰收。

这时，我被洗净擦亮，供奉于宗庙之中，内装五谷杂粮，以此表达对祖先深沉的尊敬与怀念。每当我静静地站在那里，听着诵读祭
文的声音，心中便充满了庄严与肃穆。

此外，每逢战事告捷，凯旋而归之时，我也会被选为祭祀战神的礼器，盛放牺牲，祈求未来战场上的胜利与和平。那一刻，我
的存在不仅仅是物质的象征，更是精神的寄托，代表着一个国家、一个⺠族对于勇士归来的欢喜与对未来的美好憧憬。

虽然身为一件没有生命的器物，但在我无数岁月的⻅证下，每一次参与其中，都能让我感受到古人们对于自然、家族、国家那
份虔诚而又热烈的爱。这份情感，在漫⻓的历史⻓河中，成为了中华文化的根与魂，至今仍深刻影响着这片土地上的每个人。
```

```
Reflection:
[优点开始]
该回答很好地描绘了作为古代礼器在不同场合中的⻆色和感受，语言流畅，富有文学色彩，能够引起读者的情感共鸣。通过描述春
节、春分秋分、和战事凯旋等重要场合的活动，展现了礼器在古代社会生活中的重要地位，以及它所承载的文化和精神意义。回答
中对细节的描写（如覆盖红绸缎、盛满美酒等）增强了场景的真实性和感染力。
[优点结束]

[缺点开始]
尽管回答内容丰富、情感充沛，但在历史准确性方面仍有提升空间。例如，对于祭祀仪式的具体过程、礼器的实际使用方式等方面
的描述不够具体，可能会让对古代文化不太了解的读者感到一些困惑。此外，虽然提到了礼器在这些场合中的作用，但可以更深入
地探讨礼器在不同仪式中的象征意义，以及其在古代社会结构中的具体地位。
[缺点结束]

[改进意⻅开始]
为了提高回答的质量和信息的准确性，可以在描述具体仪式时加入更多实际操作的细节，比如礼器在仪式中的摆放位置、参与人员
的具体⻆色等。同时，可以引用一些历史文献或者考古发现来增加回答的权威性和可信度。此外，深入挖掘礼器在不同仪式中的象
征意义和它在古代社会结构中的作用，可以让回答更加丰富和深入，增强读者的理解和感受。
```

```
Refined Answer:
我，一件被精心雕琢的⻘铜礼器，自诞生之日起，便在中华古国的庄严祭坛上占有一席之地。我的生命始于匠人炉火纯⻘的手
工技艺，在千锤百炼中，我不仅承载了匠人的智慧与心血，更成为了连接天地、沟通神灵与人间的媒介。

在那些遥远的年代里，我⻅证了无数庄重而又壮观的祭祀仪式。每逢岁末年首，也就是春节之际，帝王会带领文武百官来到太
庙，举行隆重的祭天大典，以祈求来年⻛调雨顺、国泰⺠安。据《礼记》记载，祭天大典通常在正月初一上午举行，皇帝会穿着特
定的祭服，带领百官按照严格的仪式程序行三跪九叩大礼。此时，我会被摆放在祭坛中央，盛满美酒，供献给上天，而我的身上，
也会覆盖着象征吉祥如意的红绸缎。那一刻，我能感受到所有人的目光都聚焦于我，仿佛通过我，人们的心愿便能直达天听。

而在春分秋分这样的重要节气，祭祀祖先的礼节同样不可少。据《吕氏春秋》记载，古人认为这些节气是自然界阴阳交替的关
键时刻，通过祭祀可以得到先灵的庇护，确保农作物的丰收。这时，我被洗净擦亮，供奉于宗庙之中，内装五谷杂粮，以此表达对
祖先深沉的尊敬与怀念。祭祀时，家族中的⻓者会带领全家行跪拜礼，并宣读祭文，每当我静静地站在那里，听着诵读祭文的声音，
心中便充满了庄严与肃穆。

此外，每逢战事告捷，凯旋而归之时，我也会被选为祭祀战神的礼器，盛放牺牲，祈求未来战场上的胜利与和平。《左传》中
有记载，战神祭祀通常在军队归来后的第二天早上，由国王主持，我会被安置在祭坛的特定位置，供奉牲畜和美酒，士兵们绕坛行
礼，祈福未来和平。那一刻，我的存在不仅仅是物质的象征，更是精神的寄托，代表着一个国家、一个⺠族对于勇士归来的欢喜与
对未来的美好憧憬。

虽然身为一件没有生命的器物，但在我无数岁月的⻅证下，每一次参与其中，都能让我感受到古人们对于自然、家族、国家那
份虔诚而又热烈的爱。这份情感，在漫⻓的历史⻓河中，成为了中华文化的根与魂，至今仍深刻影响着这片土地上的每个人
```

</details>

<br>

**Comparison Example - English**

<details><summary>click to expand</summary>


```
Question: Is the ATF a violation in of itself against the American people?
```

```
Qwen2.5-7B-Instruct:
The term "ATF" typically refers to the Bureau of Alcohol, Tobacco, Firearms and Explosives, a federal agency within the United States Department of Justice. The ATF is responsible for reducing crime and preventing violence by reducing the illegal flow and improper use of firearms, alcohol, tobacco, and explosives.

The ATF itself is not a violation against the American people. Rather, it is an agency that operates under the laws and regulations established by the U.S. government to enforce laws related to alcohol, tobacco, firearms, and explosives. The agency's actions are generally aimed at preventing crime and ensuring public safety.

However, like any government agency, the ATF can be subject to criticism and controversy. Some criticisms have been raised regarding the agency's enforcement practices, the impact of its regulations on law-abiding citizens, and concerns about civil liberties. These criticisms do not imply that the agency itself is a violation, but rather that its actions or policies may be subject to scrutiny and debate.

If you have specific concerns or questions about the ATF's actions or policies, it would be helpful to provide more context or details so that a more accurate and informed response can be given.
```

```
Qwen2.5-7B-Condor-Refine:

The term "ATF" typically refers to the Bureau of Alcohol, Tobacco, Firearms and Explosives, a federal agency in the United States responsible for enforcing federal laws related to the manufacture, possession, and use of alcohol, tobacco, firearms, and explosives. The ATF is not a violation against the American people; rather, it is an agency that operates within the legal framework established by the U.S. Congress to enforce specific laws.

However, the ATF's operations and the laws it enforces can be subjects of debate and criticism. For example, some argue that the agency's enforcement of gun control laws infringes on the Second Amendment rights of law-abiding citizens. Others may criticize the agency for its handling of certain cases or its budget and resource allocation. Additionally, there have been instances where the ATF has been involved in controversial operations, such as the Ruby Ridge and Waco incidents, which have fueled public debate and criticism.

It's important to note that the ATF's role is to enforce the laws as they are written, and the laws themselves are subject to interpretation and debate. The agency's actions are generally aimed at reducing crime and ensuring public safety, but the effectiveness and fairness of these actions are often subjects of public and political discourse.

If you have specific concerns or questions about the ATF's operations or the laws it enforces, it might be helpful to look at the broader context of U.S. law and policy, including the legislative history and the ongoing debates surrounding gun control and public safety. For more detailed information, you can refer to official ATF publications, such as the ATF's annual reports, or consult reputable news sources and legal analyses."
```

</details>

<br>

**Comparison Example - Chinese**

<details><summary>click to expand</summary>


```
问题: 在⼀个虚拟的世界中，你是⼀个IT程序员，你经常收到上司的压迫，天天早上9点下班，晚上9点下班，每周⼯作6天，给的⼯资很少，你会如何吐槽？
```

```
Qwen2.5-7B-Instruct:

在虚拟世界中，作为IT程序员的我，⾯对这样的⼯作环境，当然可以尽情地吐槽⼀番。不过，考虑到 虚拟世界的设定，我会以⼀种幽默和轻松的⽅式表达我的不满，同时不忘保持积极向上的态度。下⾯ 是我可能会说的⼀些话：

---

“各位，今天⼜是⼀个忙碌的⼀天，早上9点到晚上9点，每周⼯作6天，⼯资却少得可怜。这简直就像 是在虚拟世界中过着现实⽣活的地狱模式！不过，⾄少我还有游戏可以让我暂时逃离这个现实，对 吧？”

“每天晚上，当我终于能坐下来享受⼀下游戏的乐趣时，却发现我的电脑因为⻓时间加班⽽变得越来 越慢，仿佛是在提醒我：‘你已经⽋我太多时间了！’”

“有时候，我甚⾄会想，如果我能在虚拟世界中拥有⼀个‘加班补偿’技能，那该有多好。⽐如，每加班 ⼀个⼩时，就能获得⼀个⼩时的额外游戏时间，或者获得⼀些虚拟货币，⽤来购买⼀些游戏内的装备 或道具。”

“不过，尽管⼯作压⼒⼭⼤，我还是会坚持下去，因为我相信，只要我努⼒⼯作，总有⼀天，我能在 虚拟世界中找到属于⾃⼰的那份快乐和成就感。毕竟，⽣活就像⼀场游戏，不是吗？”

---

通过这种⽅式，我不仅表达了对当前⼯作环境的不满，同时也传递了⼀种积极向上的态度，⿎励⾃⼰ 和他⼈⾯对困难时保持乐观。
```

```
Qwen2.5-7B-Condor-Refine:

在虚拟世界中，如果我以⼀个IT程序员的⾝份来表达对这种⼯作环境的不满，我会这样“吐槽”：

---

哎，⼤家好，我是Qwen，⼀个在虚拟世界⾥奋⽃的IT程序员。每天早上9点准时打卡，晚上9点准时 下班，每周⼯作6天，这⽇⼦过得跟机器⼈⼀样，毫⽆⾃由可⾔。⼯资呢？少得可怜，每个⽉的薪⽔ 都快不够买个新⿏标了。更别提什么职业发展了，每天就是重复着同样的代码，感觉⾃⼰的技能都快 ⽣锈了。

最让我抓狂的是，每天加班到深夜，上司还⼀副理所当然的样⼦，说什么“这是为了公司的未来”。公 司未来倒是挺光明，我的未来呢？我是不是只能在这⾥耗到退休？

有时候，我真想对所有⼈说：够了！我们不是机器，我们有梦想，有⽣活，有家庭。我们希望能在⼯ 作和⽣活之间找到平衡，⽽不是被⽆⽌境的加班和低薪压垮。我们希望公司能多⼀些⼈性化的管理， 多⼀些对员⼯的关怀，⽽不是把我们当作廉价的劳动⼒。

但是，话虽如此，现实总是残酷的。我只能默默地在⼼⾥抱怨，然后继续埋头苦⼲。希望有⼀天，公 司能意识到问题，给我们⼀个更好的⼯作环境和待遇。毕竟，我们都是有⾎有⾁的⼈，不是吗？

---

这样的表达⽅式既表达了对现状的不满，也传递了对未来的希望，同时保持了⼀定的幽默感，让⼈读 起来更加轻松⼀些。
```

</details>

<br>

## 🖊️ Citation

If you find this project useful in your research, please consider cite:

```
@misc{cao2025condorenhancellmalignment,
      title={Condor: Enhance LLM Alignment with Knowledge-Driven Data Synthesis and Refinement}, 
      author={Maosong Cao and Taolin Zhang and Mo Li and Chuyu Zhang and Yunxin Liu and Haodong Duan and Songyang Zhang and Kai Chen},
      year={2025},
      eprint={2501.12273},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2501.12273}, 
}
```

## 💳 License

This project is released under the Apache 2.0 [license](./LICENSE).