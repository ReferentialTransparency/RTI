# RTI: Machine Translation Testing via Referentially Transparent Inputs

Translation errors found by our RTI approach in [Google Translate](https://translate.google.com/#view=home&op=translate&sl=en&tl=zh-CN) and [Bing Microsoft Translator](https://www.bing.com/translator). 

We introduce a novel and widely-applicable concept: RTI (referentially transparent inputs). An RTI is a piece of text in source language that should have invariant translation in target language even in different contexts. RTI is implemented by us as a tool called <em>Purity</em>. <em>Purity</em> has successfully detected 5 kinds of translation errors: under-translation, over-translation, word/phrase mistranslation, incorrect modification, and unclear logic. We will keep updating the erroneous translations uncovered by RTI to this repo.


### Template in the translation error examples: :telescope: 
+ Row 1: error category
+ Row 2: source text (in English)
+ Row 3: target text (in Chinese)
+ Row 4: target text meaning


### Translation error categories:
+ **Under-translation**: If some parts of the source text are not translated in the target text, it is an under-translation error.
+ **Over-translation**: If some parts of the target text are not translated from word(s) of the source text or some parts of the source text are unnecessarily translated for multiple times, it is an over-translation error.
+ **Word/phrase mistranslation**: If some words or phrases in the source text is incorrectly translated in the target text, it is a word/phrase mistranslation error.
+ **Incorrect modification**: If some modifiers modify the wrong element, it is an incorrect modification error.
+ **Unclear logic**: If all the words are correctly translated but the logic of the target text is wrong, it is an unclear logic error.




### Input and output example
The input of RTI is a list of unlabeled sentences in source language. For clarity, we use an unlabeled sentence here as an example.

||
| :------------- | 
| Actress Jennifer Lawrence is also expected to star as Holmes in a movie based on Bad Blood. | 
||

The output of RTI is a list of issues. The meanings of key terminologies used in the paper are as follows:
+ **Translation error**: Mistranslation of some parts of a source text.
+ **Erroneous translation**: If a target text (<em>i.e.</em>, translation) has translation error(s), we call it an erroneous translation.
+ **Issue and erroneous issue**: An issue contains (1) an RTI and its translation; and (2) a piece of text containing the RTI (<em>i.e.</em>, container) and the container's translation. An issue is erroneous if either the RTI's or the container's translation is erroneous.

An example output of RTI's implementation, <em>Purity</em> is as follows. 

| Issue 1 |
| :------------- | 
| Actress Jennifer Lawrence is also expected to star as Holmes in a movie based on Bad Blood. |
| 女演员詹妮弗·劳伦斯也有望在一部根据《坏血》改编的电影中饰演福尔摩斯。 | 
| Holmes in a movie based on Bad Blood | 
| 福尔摩斯在电影的**基础上**坏血 |

| Issue 2 |
| :------------- | 
| Holmes in a movie based on Bad Blood | 
| 福尔摩斯在电影的基础上坏血 |
| a movie based on Bad Blood | 
| **一部**基**于**坏血的电影 |


As we can see, <em>Purity</em> reports two suspicious issues. These two issues reveal one translation error in an erroneous translation.


| logic |
| :--- |
| Holmes in a movie based on Bad Blood | 
| 福尔摩斯在电影的基础上坏血 |
| Holmes' blood becomes bad based on a movie |


### Examples of translation errors detected by <em>Purity</em>

### Google Translate

| word/phrase |
| :--- |
| In a series of pointed tweets, Trump said the economy is good, so Chevy should keep the plant, the closure of which was announced back in November. |
| 特朗普在一系列明确的推文中表示，经济状况良好，因此雪佛兰应保留该工厂，该工厂已于11月宣布关闭。 |
| In a series of clear tweets, Trump said the economy is good, so Chevy should keep the plant, the closure of which was announced back in November. |

| under |
| :--- |
| the sorts of problems we work on and the almost anxiety provoking magnitude of data with which we get to work |
| 我们正在研究的各种问题以及几乎令人焦虑的数据 |
| the sorts of problems we work on and the almost anxiety provoking data with which we get to work |

| over \| logic |
| :--- |
| Covering a memorial service in the nation's capital and then traveling to Texas for another service as well as a funeral train was an honor |
| 荣幸地报道了该国首都的追悼会，然后前往得克萨斯州进行另一项服务以及葬礼列车，这是一种荣幸 |
| It was an honor to cover a memortial service of the nation's captial and then traveling to Texas to conduct another service and a funeral train was an honor.|

| word/phrase |
| :--- |
| Advertisers who are not creating housing , employment or credit ads |
| 未制作住房，就业或信用广告的广告客户 |
| Advertisers who are not building houses, employment or credit ads |

| modification |
| :--- |
| underfunded and overcrowded bottom tier , open access colleges |
| 底层资金不足，人满为患的开放式大学 |
| bottom tier is underfunded, overcrowded open access colleges |

| logic |
| :--- |
| In a world of perceived foes, Trump has often looked to leaders who mimic his own brashness and disregard for political norms as allies. |
| 在一个充满敌意的世界中，特朗普经常寻找那些模仿自己的傲慢并无视政治规范作为盟友的领导人。 |
| In a world of perceived foes, Trump has often looked to those who mimic his own brashness and disregard for political norms as allies' leaders. |

| under \| over \| logic |
| :--- |
| Children in the top 1% of families were 77 times more likely to attend these institutions than children from parents in the bottom fifth of earners, the analysis found. |
| 分析发现，在收入最高的五分之一家庭中，收入最高的五分之一家庭中的孩子比进入父母的孩子高77倍。 |
| In the top fifth of families, children in the top fifth of families were 77 times higher than children attending parents, the analysis found. |

:point_right: More translation errors in Google Translate detected by <em>Purity</em> can be found [here](errorsgoogle.md).

### Bing Microsoft Translator


| under |
| :--- |
| It's not just a matter of sending money their way. |
| 这不仅仅是送钱的问题。 |
| It's not just a matter of sending money. |

| over |
| :--- |
| our goal of a truly European banking sector |
| 我们的目标是建立一个真正的欧洲银行业 |
| our goal is to build a truly European banking sector |

| word/phrase |
| :--- |
| the General Motors plant |
| 通用汽车公司 |
| the General Motors company |

| modification |
| :--- |
| more specific skill sets that are better suited for a lot of business problems |
| 更具体的技能集，更适合于许多业务问题 |
| more specific skill sets, better suited for a lot of business problems |

| logic |
| :--- |
| approval on two separate occasions |
| 批准两个不同的场合 |
| approve two separate occasions |

| word/phrase \| modification |
| :--- |
| The South has emerged as a hub of new auto manufacturing by foreign makers thanks to lower manufacturing costs and less powerful unions. |
| 由于制造成本降低和工会实力减弱，韩国已成为外国制造商新的汽车制造中心。 |
| South Korea has emerged as a new hub of auto manufacturing by foreign makers thanks to the reduction of manufacturing costs and the weakening of unions' power. |



:point_right: More translation errors in Bing Microsoft Translator detected by <em>Purity</em> can be found [here](errorsbing.md).

