# 文明6 伟人 Mod 完整效果事实提取

> 数据来源：/tmp/civ6mod/ 下 7 个 mod 的源数据文件（.sql/.xml）直接提取，用于补全《文明6伟人mod全景分析与移植蓝图》中被"…"截断或标"—"的记录。
> 格式：伟人名 | 时代 | 完整效果（含数值）| 效果实现方式。
> 所有效果文本均为 mod 文件中的英文原文翻译/直录，数值取自 ModifierArguments / SQL 参数。

## 数据缺失/需说明的记录

1. **Sumus Magnus - Francesco Bartolomeo Rastrelli**：源文件中**没有**普通工程师版定义，只有 Urban Complexity 联动版（`X_URBAN_COMPLEXITY_Rastrelli.xml`），且该版本中他的类别是**大艺术家**（工业时代），效果是政府广场建筑+4文化。文档中"工程师 | 工业 | —"的记录在源数据里不存在对应形态。
2. **Team PVP 大音乐家**：分析文档所列"阿里斯托芬/沃尔夫拉姆/纪尧姆·德·马肖/蒙特威尔第/杜阿尔特·罗博"与 mod 实际文本**完全不符**。mod 实际 5 位音乐家是：俞伯牙、李隆基、关汉卿、汤应曾、托马斯·路易斯（见下文 §1）。
3. **Team PVP 巨作数量**：文艺复兴作家每人只产 **1** 部巨作（SQL 中 `GreatWorksNum=1`），中世纪音乐家每人只产 **1** 部；其余时代作家/音乐家每人 2 部。文档"各产两部"的假设不成立。
4. **Sumus Magnus - "西塞罗"（内部代号 CICERO）**：实际显示名为 **Mahbub ul Haq**（LOC 文本与 Pedia 均为此人），但两件巨作名是西塞罗的著作；"罗伯特·舒曼"（代号 DESCARTES）的巨作名则是笛卡尔的著作。作者人名与巨作混搭，如实记录。
5. **Nyguita - Eumenes / Wallenstein / Túpac Yupanqui / Kountouriotis** 四人：源数据使用**原版**修饰器 `GREATPERSON_GOVERNOR_POINTS`（+1 总督头衔），mod 内无自定义文本。
6. **Nyguita - Sergius Orata**：使用原版修饰器 `GREATPERSON_CITY_HOUSING_SMALL`（+2 住房）+ `GREATPERSON_CITY_AMENITIES_SMALL`（+1 宜居）。
7. Sumus Magnus 的专属建筑（Templar Vault / Paper Maker / Chocolaterie）、专属资源（Pepper/Nutmeg/Faberge Egg/Praline/Beaver）、可解锁改良（Chateau/Mission/Polder）为伟人效果的依赖物，已在对应行注明。

---

## 1. Team PVP More GreatPeople 伟人补充包（3497524344）

实现方式：纯 SQL 巨作表（`GreatWorks` + `GreatWork_YieldChanges`），著作/乐曲基础产出 4 文化 + 旅游（文艺复兴作家 4 文化 1 部；音乐家文艺复兴 2 部各 4 文化，中世纪 1 部）。无修饰器、无 Lua。

### 大作家（23 位）——每人巨作

| 伟人 | 时代 | 巨作 | 实现方式 |
|---|---|---|---|
| 宋玉 | 古典 | 《九辩》《高唐赋》 | 纯SQL巨作 |
| 司马相如 | 古典 | 《子虚赋》《上林赋》 | 纯SQL巨作 |
| 班固 | 古典 | 《汉书》《两都赋》 | 纯SQL巨作 |
| 谢灵运 | 古典 | 《山居赋》《登池上楼》 | 纯SQL巨作 |
| 杜甫 | 中世纪 | 《三吏三别》《秋兴八首》 | 纯SQL巨作 |
| 白居易 | 中世纪 | 《长恨歌》《琵琶行》 | 纯SQL巨作 |
| 辛弃疾 | 中世纪 | 《青玉案·元夕》《永遇乐·京口北固亭怀古》 | 纯SQL巨作 |
| 苏轼 | 中世纪 | 《赤壁赋》《赤壁怀古》 | 纯SQL巨作 |
| 罗贯中 | 文艺复兴 | 《三国演义》（仅1部） | 纯SQL巨作 |
| 施耐庵 | 文艺复兴 | 《水浒传》（仅1部） | 纯SQL巨作 |
| 吴承恩 | 文艺复兴 | 《西游记》（仅1部） | 纯SQL巨作 |
| 曹雪芹 | 文艺复兴 | 《红楼梦》（仅1部） | 纯SQL巨作 |
| 梁启超 | 工业 | 《少年中国说》《饮冰室合集》 | 纯SQL巨作 |
| 雨果 | 工业 | 《悲惨世界》《巴黎圣母院》 | 纯SQL巨作 |
| 托尔斯泰 | 工业 | 《战争与和平》《安娜·卡列尼娜》 | 纯SQL巨作 |
| 海明威 | 现代 | 《老人与海》《太阳照常升起》 | 纯SQL巨作 |
| 鲁迅 | 现代 | 《呐喊》《彷徨》 | 纯SQL巨作 |
| 茅盾 | 现代 | 《蚀》《子夜》 | 纯SQL巨作 |
| 老舍 | 原子能 | 《骆驼祥子》《四世同堂》 | 纯SQL巨作 |
| 沈从文 | 原子能 | 《边城》《长河》 | 纯SQL巨作 |
| 刘慈欣 | 信息 | 《三体》《流浪地球》 | 纯SQL巨作 |
| 莫言 | 信息 | 《红高粱》《生死疲劳》 | 纯SQL巨作 |
| 江南 | 信息 | 《龙族》《九州缥缈录》 | 纯SQL巨作 |

### 大音乐家（5 位，实际人名与文档不同）——每人巨作

| 伟人 | 时代 | 巨作 | 实现方式 |
|---|---|---|---|
| 俞伯牙 | 古典 | 《高山》《流水》 | 纯SQL巨作 |
| 李隆基 | 中世纪 | 《霓裳羽衣曲》（仅1部） | 纯SQL巨作 |
| 关汉卿 | 中世纪 | 《窦娥冤》（仅1部） | 纯SQL巨作 |
| 汤应曾 | 文艺复兴 | 《十面埋伏》《洞庭秋思》 | 纯SQL巨作（各4文化4旅游） |
| 托马斯·路易斯 | 文艺复兴 | 《王国多么荣耀》《悼亡仪式》 | 纯SQL巨作（各4文化4旅游） |

---

## 2. Nyguita More Great People 更多伟人（2559462758）

实现方式：全部为 XML 数据库修饰器（GreatPersonIndividualActionModifiers + Modifiers + ModifierArguments + 单位能力），无 Lua。大将军/大海军统帅另带原版同代光环（+5力+1移动力，2格）。

### 大将军（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Eumenes of Cardia | 古典 | +1 总督头衔 | 原版修饰器 GREATPERSON_GOVERNOR_POINTS |
| Zhuge Liang（诸葛亮） | 古典 | 触发"军事战术"尤里卡；若已触发则直接完成该科技。另赠予1个陆军军事单位永久能力：战斗经验+25% | XML修饰器（科技推进+单位能力） |
| Jan Žižka | 中世纪 | 所有陆地单位防御时 +5 战斗力（永久能力，覆盖全部陆军类别） | XML修饰器+单位能力 |
| Roger de Flor | 中世纪 | 在拥有总督的城市购买陆地军事单位时，金币与信仰价格 -10%（永久） | XML修饰器（购价折扣） |
| Tomoe Gozen | 中世纪 | 立即创建1个带1级晋升的 Courser（追击者）单位 | XML修饰器（赠单位带经验） |
| Albrecht von Wallenstein | 文艺复兴 | +1 总督头衔 | 原版修饰器 GREATPERSON_GOVERNOR_POINTS |
| Federico da Montefeltro | 文艺复兴 | 每部著作巨作 +1 科技；每件艺术巨作（宗教/雕塑/肖像/风景）+1 文化（永久，全城市） | XML修饰器（巨作产出加成×5条） |
| Hernán Cortés | 文艺复兴 | 立即创建1个带1级晋升的西班牙征服者单位 | XML修饰器（赠单位带经验） |
| Geronimo | 工业 | 与基础战斗力高于自己的敌人作战时 +5 战斗力（永久能力，全部陆军类别） | XML修饰器+单位能力（依赖拜占庭/高卢包需求条件） |
| Hijikata Toshizō | 工业 | 该城市每回合 +4 忠诚度 | XML修饰器（单城忠诚/回合） |
| Emiliano Zapata | 现代 | 劫掠改良设施与劫掠区域获得的收益翻倍（永久） | XML修饰器（劫掠收益×2） |

### 大海军统帅（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Grace O'Malley | 文艺复兴 | 获得 100 金币；海岸劫掠收益 +75%（永久能力，含对改良设施） | XML修饰器（一次性金币+劫掠能力） |
| Hasekura Tsunenaga | 文艺复兴 | 通往更先进文明的商路：对方每领先5项科技 +1 科技，每领先5项市政 +1 文化（永久） | XML修饰器（商路产出） |
| Michiel de Ruyter | 文艺复兴 | 1个海军单位 +7 战斗力（永久能力） | XML修饰器+单位能力 |
| Peter Tordenskjold | 文艺复兴 | 海军单位攻击区域防御时 +5 战斗力（永久能力） | XML修饰器+单位能力 |
| Túpac Yupanqui | 文艺复兴 | +1 总督头衔 | 原版修饰器 GREATPERSON_GOVERNOR_POINTS |
| Vasco da Gama | 文艺复兴 | 提供 2 份香料资源；商路起点与目的地双方金币 +50%（永久） | XML修饰器（资源+商路金币×2条） |
| David Farragut | 工业 | 该城市每回合 +4 忠诚度 | XML修饰器（单城忠诚/回合） |
| Fernando Villaamil | 工业 | 立即创建1艘驱逐舰；每回合 +1 石油 | XML修饰器（赠单位+资源/回合） |
| James Cook | 工业 | 每个你为其宗主国的城邦：+2 科技、+2 文化、+2 金币（永久） | XML修饰器（城邦产出×3条） |
| Pavlos Kountouriotis | 现代 | +1 总督头衔 | 原版修饰器 GREATPERSON_GOVERNOR_POINTS |
| Jacques-Yves Cousteau | 原子能 | 获得 1000 文化；珊瑚礁地块 +2 文化（永久） | XML修饰器（一次性文化+地块产出） |

### 大科学家（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Hippocrates | 古典 | 指定城市 +1 住房；所有城市增长 +5%（永久） | XML修饰器（住房+全局增长） |
| Sun Simiao（孙思邈） | 古典 | 无需科技要求直接揭示硝石资源；另触发1个随机中世纪科技尤里卡 | XML修饰器（资源揭示+原版随机尤里卡） |
| Roger Bacon | 中世纪 | 触发"科学理论"尤里卡，若已触发则直接完成该科技；从所有来源获得的大科学家点数 +20%（永久） | XML修饰器（科技推进+伟人点加成） |
| Gerardus Mercator | 文艺复兴 | 海军单位与乘船单位 +1 移动力（永久）；触发"制图学"尤里卡，若已触发则直接完成该科技 | XML修饰器（移动力+科技推进） |
| Paracelsus von Hohenheim | 文艺复兴 | 大学 +2 食物、+2 金币、+1 住房（永久） | XML修饰器（建筑产出×3条） |
| Ulugh Beg | 文艺复兴 | 宫殿及政府广场、外交区的所有建筑（含女王图书馆、领事馆、官邸）各 +3 科技（永久，共13条建筑加成） | XML修饰器（建筑产出×13条） |
| John Muir | 工业 | 魅力为"惊艳"的地块 +1 科技、+1 文化（永久）；赠予1个自然学家单位 | XML修饰器（地块产出+赠单位） |
| Auguste Piccard | 现代 | 触发"飞行"与"高级飞行"尤里卡；若"飞行"已触发则直接完成该科技（高级飞行不直接完成）；隐形单位与攻城射程支援单位 +1 视野（永久能力） | XML修饰器（双科技推进+单位能力） |
| Edith Clarke | 现代 | 电力充足的城市 +5% 科技（永久） | XML修饰器（通电城市科技%） |
| Jagadish Chandra Bose | 现代 | 触发"无线电"与"电信"尤里卡，若已触发则直接完成对应科技；另触发1个随机现代科技尤里卡 | XML修饰器（双科技推进+原版随机尤里卡） |
| Rachel Carson | 原子能 | 所在格及相邻格每块海岸：+250 科技、+200 文化（一次性） | XML修饰器（按海岸格给科技/文化） |

### 大工程师（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Archimedes | 中世纪 | 该城市每回合额外 +1 次远程攻击；立即创建1台投石机 | XML修饰器（城防攻击次数+赠单位） |
| Master Gerhard | 中世纪 | 给予 350 点奇观建造生产力；奇观 +3 信仰（永久） | XML修饰器（奇观锤+奇观产出） |
| Sergius Orata | 中世纪 | 该城市 +2 住房、+1 宜居度 | 原版修饰器（HOUSING_SMALL+AMENITIES_SMALL） |
| Bartolomeo Cristofori | 文艺复兴 | 工坊 +1 大音乐家点数，并获得1个音乐巨作槽（永久） | XML修饰器（伟人点+建筑槽位） |
| Orbán | 文艺复兴 | 攻城单位 +15% 生产力（永久）；攻城单位对可防御区域 +5 战斗力（永久能力） | XML修饰器+单位能力 |
| Henry Bessemer | 工业 | 触发"钢铁"尤里卡，若已触发则直接完成该科技；建筑 +10% 生产力（永久，不含奇观） | XML修饰器（科技推进+建筑锤%） |
| Joseph-Marie Jacquard | 工业 | 立即建成1座工坊和1座工厂；该城市 +2 电力 | 原版修饰器（工坊/工厂）+XML（免费电力） |
| Norbert Rillieux | 工业 | 种植园 +2 食物、+2 金币、+1 生产力（永久） | XML修饰器（改良产出） |
| Hugo Eckener | 现代 | 飞机 +1 移动力、+1 航程（永久能力） | XML修饰器+单位能力×2 |
| Sakichi Toyoda | 现代 | 工业区的生产力邻接加成同时提供等量科技（永久） | XML修饰器（邻接映射） |
| Nikolay Dollezhal | 原子能 | 每回合 +1 铀；核项目（曼哈顿计划/常春藤行动/建造核装置/建造热核装置）+25% 生产力（永久） | XML修饰器（资源/回合+项目锤%×4条） |

### 大商人（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Gaius Maecenas | 古典 | 用金币赞助伟人时费用 -10%（永久） | XML修饰器（赞助折扣） |
| Wang Anshi（王安石） | 中世纪 | +1 经济政策槽（任意政体） | XML修饰器（政策槽） |
| Antonio Van Diemen | 文艺复兴 | 通往外国大陆的国际商路 +1 食物、+1 生产力、+2 金币（永久） | XML修饰器（跨洲商路产出×3条） |
| Jerome Horsey | 文艺复兴 | +1 外交政策槽（任意政体） | XML修饰器（政策槽） |
| Pierre-Esprit Radisson | 文艺复兴 | 创造 1 份"海狸"专属奢侈品（+2 宜居度）；营地 +1 金币、+1 生产力（永久） | XML修饰器（专属资源+改良产出；依赖mod自带海狸资源） |
| Samuel de Champlain | 文艺复兴 | 立即创建1个开拓者和1个火枪手 | XML修饰器（赠双单位） |
| Elizabeth Macarthur | 工业 | 牧场触发文化炸弹；牧场 +2 金币（永久） | XML修饰器（文化炸弹+改良产出） |
| Ninomiya Sontoku | 工业 | 农场与梯田 +1 金币（永久）；拥有已就职总督的城市：该总督每有1级晋升 +2% 金币（永久） | XML修饰器（改良产出+总督条件加成） |
| Thomas Cook | 工业 | 世界奇观、海滨度假村、滑雪场的旅游业绩 +50%（永久） | XML修饰器（旅游%×3条，ScalingFactor=150） |
| Solomon R. Guggenheim | 现代 | 一次性：此城每件艺术巨作（宗教/雕塑/肖像/风景）给予 350 金币；此后每件艺术巨作 +2 金币（永久） | XML修饰器（按巨作给金×4+巨作产出×4条） |
| Satoru Iwata | 信息 | 研究实验室 +3 文化、+2 金币、-1 科技；商业中心 +1 宜居度（永久） | XML修饰器（建筑产出×3+区域宜居） |

### 大作家（11 位）——每人 2 部著作

| 伟人 | 时代 | 巨作 | 实现方式 |
|---|---|---|---|
| Lucian | 古典 | 《Lover of Lies》《A True Story》 | 纯巨作 |
| Al-Hariri of Basra | 中世纪 | 《Serugium》《Response to a stranger's request》 | 纯巨作 |
| Chrétien de Troyes | 中世纪 | 《Lancelot, the Knight of the Cart》《Perceval, the Story of the Grail》 | 纯巨作 |
| Christine de Pizan | 文艺复兴 | 《To sing a happy song with a sad heart》《The Book of the City of Ladies》 | 纯巨作 |
| Jules Verne | 工业 | 《Journey to the Center of the Earth》《Around the World in Eighty Days》 | 纯巨作 |
| Victor Hugo | 工业 | 《The Hunchback of Notre-Dame》《Les Misérables》 | 纯巨作 |
| Jorge Luis Borges | 现代 | 《The Garden of Forking Paths》《Death and the Compass》 | 纯巨作 |
| Osamu Dazai | 现代 | 《The Setting Sun》《No Longer Human》 | 纯巨作 |
| Sir Arthur Conan Doyle | 现代 | 《The Sign of Four》《The Hound of the Baskervilles》 | 纯巨作 |
| Umberto Eco | 原子能 | 《The Name of the Rose》《Foucault's Pendulum》 | 纯巨作 |
| Kinoko Nasu | 信息 | 《Tsukihime》《Fate/Stay Night》 | 纯巨作 |

### 大艺术家（11 位）——每人 3 件艺术品

| 伟人 | 时代 | 巨作 | 实现方式 |
|---|---|---|---|
| Giuseppe Arcimboldo | 文艺复兴 | 《The Jurist》《Summer》《Vertumnus》 | 纯巨作 |
| Nicolas Poussin | 文艺复兴 | 《The Martyrdom of Saint Erasmus》《The Shepherds of Arcadia (Et in Arcadia Ego)》《The Judgement of Solomon》 | 纯巨作 |
| Antonio Canova | 工业 | 《Psyche Revived by Cupid's Kiss》《Venus Victrix》《The Three Graces》 | 纯巨作 |
| Edgar Degas | 工业 | 《The Orchestra at the Opera》《The Star》《Little Dancer Aged Fourteen》 | 纯巨作 |
| Katsushika Ōi | 工业 | 《Beauty Fulling Cloth in the Moonlight》《Nightscene in the Yoshiwara》《Mount Fuji through a Bamboo Forest》 | 纯巨作 |
| Alphonse Mucha | 现代 | 《Zodiac》《Nature》《After the Battle of Grunwald》 | 纯巨作 |
| Amedeo Mogigliani | 现代 | 《The Cellist》《Head》《Jeanne Hébuterne aux épaules nues》 | 纯巨作 |
| Camille Claudel | 现代 | 《Sakuntala》《The Waltz》《The Mature Age》 | 纯巨作 |
| Jean-Michel Basquiat | 原子能 | 《Slave Auction》《Untitled》《Sabado por la Noche》 | 纯巨作 |
| Salvador Dalí | 原子能 | 《The Persistence of Memory》《Galatea of the Spheres》《Crucifixion (Corpus Hypercubus)》 | 纯巨作 |
| Peter Doig | 信息 | 《Camp Forestia》《Echo Lake》《100 Years Ago》 | 纯巨作 |

### 大音乐家（11 位）——每人 2 部乐曲

| 伟人 | 时代 | 巨作 | 实现方式 |
|---|---|---|---|
| Barbara Strozzi | 文艺复兴 | 《Il primo libro di madrigali: Amor Amor》《Diporti di Euterpe ovvero Cantate e ariette a voce sola》 | 纯巨作 |
| Richard Wagner | 工业 | 《Tannhäuser Ouverture》《Ride Of The Valkyries》 | 纯巨作 |
| Giacomo Puccini | 现代 | 《Madame Butterfly: Un bel di vedremo》《Turandot: Nessun Dorma》 | 纯巨作 |
| Ulvi Cemal Erkin | 现代 | 《Duyuşlar (Impressions for piano) No.1 Oyun / Game》《Köçekçe, Dance Rhapsody for orchestra》 | 纯巨作 |
| Benjamin Britten | 原子能 | 《The Young Person's Guide to the Orchestra》《War Requiem - Dies Irae》 | 纯巨作 |
| Iannis Xenakis | 原子能 | 《Metastasis》《Pléïades: Peaux》 | 纯巨作 |
| Louis W. Ballard | 原子能 | 《Katcina Dances Mvt.4: Bees》《Incident at Wonded Knee》 | 纯巨作 |
| Olivier Messiaen | 原子能 | 《Quartet for the End of Time: Mvt.1 Liturgie de Cristal》《Four Rhythmic Etudes: Mvt. 4 Île de feu》 | 纯巨作 |
| Steve Reich | 原子能 | 《Clapping Music》《Music for 18 Musicians: Pulses》 | 纯巨作 |
| Georg Friedrich Haas | 信息 | 《String Quartet No. 2》《Limited Approximations: Mvt. 3》 | 纯巨作 |
| Yūgo Kanno | 信息 | 《Trombone Concerto Flower : Mvt 3, Flower Note》《Symphony No.2 "Alles ist Architektur"》 | 纯巨作 |

---

## 3. Sumus Magnus Great People Expansion 伟人扩展（2448605286）

实现方式：XML 数据库修饰器 + 单位能力（被动光环），无 Lua。部分伟人依赖 mod 自带专属建筑（圣殿骑士金库/造纸坊/巧克力工坊）、专属资源（胡椒/肉豆蔻/彩蛋/果仁糖）、或解锁建造者改良（城堡/传教团/圩田）。注意：mod 内部代号与实际人名大量错位（下文按**实际显示名**记录）。

### 大将军（16 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Baibars | 中世纪 | 单位受伤造成的战斗力削减降低 20%（永久）；被动：中世纪与文艺复兴时代陆军单位在2格范围内每回合结束时回复生命（即使移动或攻击后） | XML修饰器+被动光环能力 |
| Gajah Mada | 中世纪 | 给予此城 1 份"胡椒"资源；若此城被征服，额外给予"肉豆蔻"，两者各提供 +4 宜居度。被动：中世纪与文艺复兴陆军单位乘船时 +10 战斗力，且上船/下船不消耗移动力 | XML修饰器（专属资源×2）+双被动能力 |
| Hugues de Payens | 中世纪 | 解锁并立即建成"圣殿骑士金库"（Templar Vault）——专属建筑，提供等同于该城信仰产出 10% 的金币；被动：中世纪与文艺复兴陆军单位击杀敌人时产生信仰 | XML修饰器+专属建筑（依赖mod建筑）+被动能力 |
| Jan Žižka | 中世纪 | 陆地单位与基础战斗力更高的单位作战时 +4 战斗力（永久能力）；被动：中世纪与文艺复兴非远程陆军单位防御远程攻击时 +10 战斗力 | XML修饰器+双被动能力 |
| Khalid ibn al-Walid | 中世纪 | 获得 200 信仰；被动：2格范围内的中世纪与文艺复兴陆军单位对宗教敌人 +7 战斗力 | XML修饰器（一次性信仰）+被动光环能力 |
| Rurik | 中世纪 | 立即创建1个开拓者和1个狂战士；被动：中世纪与文艺复兴陆军单位经验获取 +80% | XML修饰器（赠双单位）+被动能力 |
| Carolus Rex | 文艺复兴 | 允许训练 Carolean（卡洛琳步兵）（需"金属铸造"科技）；被动：文艺复兴与工业时代陆军单位每点未使用移动力 +3 战斗力 | XML修饰器（解锁UU）+被动能力 |
| Catherina Sforza | 文艺复兴 | 获得 300 文化 | XML修饰器（一次性文化） |
| Hernán Cortés | 文艺复兴 | 创建1个带1级晋升的西班牙征服者；被动：中世纪与文艺复兴近战陆军单位有几率转化被击败的敌单位 | XML修饰器（赠单位带经验）+被动能力 |
| Stanisław Żółkiewski | 文艺复兴 | 允许训练翼骑兵（需"重商主义"市政）；被动：中世纪与文艺复兴骑兵单位攻击时 +7 战斗力 | XML修饰器（解锁UU）+被动能力 |
| Giuseppe Garibaldi | 工业 | 近战单位在你首都所在大陆作战时 +3 战斗力（永久能力） | XML修饰器+单位能力 |
| Lawrence of Arabia | 现代 | 解放城市后：所有城市 +20% 文化，持续10回合 | XML修饰器（解放触发的限时产出） |
| Roman von Ungern-Sternberg | 现代 | 立即创建 5 个怯薛（Keshig）单位 | XML修饰器（赠单位×5） |
| Ulysses S. Grant | 现代 | +1 外交胜利点 | XML修饰器（外交胜利点） |
| William Lendrum Mitchell | 现代 | 航空港及其建筑建成时赠予1个免费的战斗机类单位复制；这些免费单位对区域防御无远程战力惩罚 | XML修饰器（区域建筑赠空军单位） |
| Carl Gustaf Emil Mannerheim | 原子能 | 所有陆地单位防御时 +4 战斗力（永久能力） | XML修饰器+单位能力 |

### 大海军统帅（8 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Agrippa | 古典 | 给予 245 点奇观建造生产力 | XML修饰器（奇观锤） |
| Ragnar Lodbrok | 中世纪 | 劫掠改良设施获得的收益翻倍（永久）；被动：中世纪与文艺复兴海军近战单位可俘获被击败的敌海军单位 | XML修饰器+被动能力 |
| Roger of Lauria | 中世纪 | 海军近战单位每点未使用移动力 +1 战斗力（永久能力） | XML修饰器+单位能力 |
| Afonso de Albuquerque | 文艺复兴 | 若此城建在非首都所在大陆，给予此城 1 份"肉豆蔻"资源；黄金时代改为给予 2 份（各 +4 宜居度） | XML修饰器（条件性专属资源） |
| Andrea Doria | 文艺复兴 | 海军近战单位征服城市时将其转化为你的主流宗教（永久能力） | XML修饰器+单位能力 |
| Hayreddin Barbarossa | 文艺复兴 | 允许训练巴巴里海盗船（需"中世纪集市"市政）；被动：文艺复兴与工业时代海军近战单位可俘获被击败的敌海军单位 | XML修饰器（解锁UU）+被动能力 |
| Henry Morgan | 文艺复兴 | 获得 1 个总督头衔（或招募1名新总督）；被动：文艺复兴与工业时代海军近战单位可俘获被击败的敌海军单位 | 原版修饰器（总督头衔）+被动能力 |
| Michiel de Ruyter | 文艺复兴 | 指定城市每回合额外 +1 次远程攻击 | XML修饰器（城防攻击次数） |

### 大科学家（10 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Aristotle | 古典 | 任意政体 +1 万能政策槽 | XML修饰器（政策槽） |
| Cai Lun（蔡伦） | 古典 | 解锁并立即建成"造纸坊"（Paper Maker）——专属建筑，+1 科技、+2 金币 | XML修饰器+专属建筑（依赖mod建筑） |
| Averroes | 中世纪 | 黄金时代期间：每部著作巨作 +1 科技、+2 信仰（永久，条件触发） | XML修饰器（巨作产出×2条，黄金时代条件） |
| Avicenna | 中世纪 | 触发1个随机中世纪科技尤里卡；宗教单位神学战斗 +3 战斗力（永久能力） | 原版随机尤里卡+单位能力 |
| Shen Kuo（沈括） | 中世纪 | 该学院区域的科技邻接加成同时提供等量生产力（永久） | XML修饰器（邻接映射） |
| Christopher Clavius | 文艺复兴 | 获得等同于当前信仰产出 50% 的一次性科技值；允许你的建造者建造"传教团"改良（需"教育"科技） | XML修饰器（信仰转科技0.5系数）+解锁改良 |
| Erasmus | 文艺复兴 | 不与任何文明交战时：每座大学 +1 外交支持/回合（永久）；触发1个随机中世纪或文艺复兴市政鼓舞 | XML修饰器（建筑外交支持）+原版随机鼓舞 |
| Louis Pasteur | 工业 | 所有城市 +20% 增长（永久）；触发"卫生设备"尤里卡，若已触发则直接完成该科技 | XML修饰器（全局增长+科技推进） |
| Michael Faraday | 工业 | 指定城市每回合 +2 电力；触发1个随机工业时代科技尤里卡；2 次使用次数 | XML修饰器（免费电力+原版随机尤里卡），ActionCharges=2 |
| Andrei Sakharov | 信息 | +1 外交胜利点；触发1个随机原子能或信息时代科技尤里卡 | XML修饰器（外交胜利点+随机尤里卡） |

### 大工程师（12 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Apollodorus of Damascus | 中世纪（另有古典版） | 该城每个区域 +1 生产力、+1 文化（永久） | XML修饰器（区域产出×2条） |
| Muhammad V | 中世纪 | 为首都宫殿增加 3 个艺术巨作槽；放置在宫殿的宗教艺术巨作 +4 信仰（永久） | XML修饰器（宫殿槽位+巨作产出） |
| Phidias | 中世纪（另有古典版） | 此城所有古典时代奇观各增加 1 个万能巨作槽（可放圣物/文物/雕塑类；覆盖12座指定古典奇观） | XML修饰器（奇观槽位×12条） |
| Vitruvius | 中世纪（另有古典版） | 触发"工程学"与"军事工程学"尤里卡，已触发则直接完成对应科技；被动：古典与中世纪攻城单位 +5 战斗力 | XML修饰器（双科技推进）+被动能力 |
| Jan Adriaanszoon Leeghwater | 文艺复兴 | 指定城市免疫环境损害（洪水/风暴等）；允许你的建造者建造"圩田"改良（需"公会"市政） | XML修饰器（免环境损害）+解锁改良 |
| Philibert de l'Orme | 文艺复兴 | 指定工业区的生产力邻接加成提供等量文化；允许你的建造者建造"城堡"改良（需"人文主义"市政） | XML修饰器（邻接映射）+解锁改良 |
| Urban | 文艺复兴 | 立即创建2台各带1级晋升的射石炮（可部署于任意位置） | XML修饰器（赠双单位带经验） |
| Vauban | 文艺复兴 | 立即创建1个军事工程师；堡垒为工业区提供 +1 生产力邻接加成（永久） | XML修饰器（赠单位+改良邻接产出） |
| Alfred Krupp | 工业 | 攻城单位 +25% 生产力（永久） | XML修饰器（单位锤%） |
| Francesco Bartolomeo Rastrelli | 工业 | 〔仅 Urban Complexity 联动版，类别为大艺术家〕此城的 Cabinet、Mansion 及政府广场建筑各 +4 文化（永久） | XML修饰器（建筑产出×12条，依赖UC联动） |
| Isambard Kingdom Brunel | 工业 | 指定城市：每有一种已建成的区域类型 +1% 生产力（永久，按16种区域逐一判定） | XML修饰器（按区域类型%×16条） |
| Alberto Santos-Dumont | 现代 | 航空港从每个相邻区域获得 +2 生产力、+2 文化（永久） | XML修饰器（区域邻接产出×2条） |

### 大商人（12 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Croesus | 古典 | 当前国库金币翻倍 | XML修饰器（国库×2，参数100%） |
| Bon da Malamocco | 中世纪 | 在外国港口激活：赠予1件免费圣物，且商路容量 +1 | XML修饰器（圣物+原版商路容量） |
| Ibn Battuta | 中世纪 | 每条商路每经过4格 +1 信仰（永久，系数0.25/格） | XML修饰器（商路里程信仰） |
| Afanasy Nikitin | 文艺复兴 | 标准版：在外国领土激活，此城每有一种已建成区域类型给予 100 金币；联动/替代版：将所在格奢侈品复制1份赠予首都，2 次使用次数 | XML修饰器（按区域类型给金×14条 / 复制奢侈），两版本文件并存 |
| Jacob Kettler | 文艺复兴 | 指定港口的金币邻接加成额外提供等量生产力，2 次使用次数；〔More Maritime 联动版改为：赠予1个开拓者+1艘护卫舰，指定滨水区提供等同食物邻接的金币〕 | XML修饰器（邻接映射），ActionCharges=2；另有联动变体 |
| Miura Anjin | 文艺复兴 | 任意政体 +1 外交政策槽 | XML修饰器（政策槽） |
| Alexander Hamilton | 工业 | 任意政体 +1 经济政策槽 | XML修饰器（政策槽） |
| Cecil Rhodes | 工业 | 立即创建1个红衣军单位；你所有位于非首都大陆且拥有总督的城市 +20% 金币（永久） | XML修饰器（赠单位+条件城市金%） |
| Jean Neuhaus II | 工业 | 解锁"巧克力工坊"（Chocolaterie）——昂贵专属建筑，提供文化并赠予1份"果仁糖"奢侈品（+4 宜居度） | XML修饰器+专属建筑（依赖mod建筑/资源） |
| Shibusawa Eiichi | 工业 | 此城每种供电资源（煤/石油/铀）为该城每种已改良奢侈品 +1 宜居度（永久） | XML修饰器（资源-宜居联动×3条） |
| John Pierpont Morgan | 现代 | 每座银行 +1 外交支持/回合（永久） | XML修饰器（建筑外交支持） |
| Peter Carl Faberge | 现代 | 创造 2 份"法贝热彩蛋"奢侈品，各 +5 宜居度 | XML修饰器（专属资源×2，依赖mod资源） |

### 大作家（10 位）

| 伟人 | 时代 | 完整效果/巨作 | 实现方式 |
|---|---|---|---|
| Augustine of Hippo | 古典 | 2部著作：《Confessions》《The City of God》（各4文化4旅游） | 纯巨作（ActionCharges=0，巨作直挂伟人） |
| Hugo Grotius | 文艺复兴 | +1 外交胜利点 | XML修饰器 |
| Friedrich Nietzsche | 工业 | 2部著作：《Thus Spoke Zarathustra》《Will to power》 | 纯巨作 |
| Jean-Jacques Rousseau | 工业 | +1 外交胜利点 | XML修饰器 |
| Voltaire | 工业 | +1 外交胜利点 | XML修饰器 |
| H. P. Lovecraft | 现代 | 2部著作：《The Call of Cthulhu》《The Shadow over Innsmouth》 | 纯巨作 |
| Martin Heidegger | 现代 | 2部著作：《Being and Time》《Poetry, language, thought》 | 纯巨作 |
| Robert E. Howard | 现代 | 2部著作：《Conan the Barbarian (Series)》《Solomon Cane (Series)》 | 纯巨作 |
| Robert Schuman（代号DESCARTES） | 原子能 | +1 外交胜利点（"和平愿景"可选包） | XML修饰器 |
| Mahbub ul Haq（代号CICERO，巨作为西塞罗著作《De Oratore》《De re publica》） | 原子能 | +1 外交胜利点（"和平愿景"可选包） | XML修饰器+巨作表 |

### 大艺术家（2 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| André Le Nôtre | 文艺复兴 | 该城所有地块 +1 魅力 | 原版修饰器 GREATPERSON_CITY_APPEAL_SMALL |
| Lancelot Brown | 工业 | 市中心每相邻1个城市公园 +2 文化；若相邻3个城市公园，额外 +3 文化（永久） | XML修饰器（改良邻接产出×2条） |

### 大探险家（JNR 联动，2 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Ahmad ibn Majid | 文艺复兴 | 所有海军单位 +2 移动力（永久能力） | XML修饰器+单位能力（依赖JNR大探险家类别） |
| Vitus Bering | 文艺复兴 | 冻土地块为港口提供 +1 金币邻接；雪原地块为港口提供 +3 文化邻接（永久） | XML修饰器（地形邻接产出×2条，依赖JNR类别） |

---

## 4. Great Sovereigns 大统治者伟人（2973448849）

实现方式：新增 GREAT_PERSON_CLASS_GreatSovereigns 类别 + 全套 XML 修饰器/单位能力；部分效果依赖 mod 专属资源（Cowrie）、专属建筑（Arsenal 等）、JNR 联动（Isabella）。招募依赖 mod 新增的专属项目/政策卡/万神殿。32 位全部效果如下（内部代号 FIRST~SIXTEENTH 等，按实际显示名记录）：

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Solomon | 古典 | 立即在此城建成1座神庙；神庙 +2 生产力（永久） | XML修饰器（赠建筑+建筑产出） |
| Marcus Aurelius | 古典 | 触发所有中世纪时代市政的鼓舞 | XML修饰器（整时代市政鼓舞） |
| Ptolemy | 古典 | 给予 100 点奇观建造生产力；每派往城邦1名使者 +1 文化（永久） | XML修饰器（奇观锤+使者产出） |
| Asoka | 古典 | 每座城市：每个专业区域 +1 信仰、+1 食物（永久） | XML修饰器（区域产出×2条） |
| Frederick II | 中世纪 | 任意政体 +1 经济政策槽 | XML修饰器（政策槽） |
| Charlemagne | 中世纪 | 任意政体 +1 军事政策槽 | XML修饰器（政策槽） |
| Harun al-Rashid | 中世纪 | 黄金时代期间：商路每经过6格 +1 科技（永久，条件触发） | XML修饰器（商路里程科技） |
| Al-Hakam II | 中世纪 | 拥有祭祀建筑的城市可额外建造1座大教堂、清真寺或会堂，不受祭祀信条限制 | XML修饰器（额外祭祀建筑×3条） |
| Alfred the Great | 中世纪 | 建造军械库（Arsenal）时赠予1个免费海军单位；军械库从相邻区域获得 +1 科技、+1 生产力（永久） | XML修饰器（建筑赠单位+邻接产出） |
| Enrico Dandolo | 中世纪 | 为首都宫殿增加 2 件圣物及圣物槽；商人单位经过外国城市地块时使该城 -20 忠诚 | XML修饰器（宫殿圣物+商队减忠诚） |
| Parameswara | 中世纪 | 指定城市每回合额外 +1 次远程攻击；每有1座港口/商业中心/外交区，该城 +5% 金币、+5% 信仰（永久） | XML修饰器（城防+按区域%产出） |
| Ramkhamhaeng | 中世纪 | 你每宗主1种不同类型的城邦，所有城市 +1 人口（按6种城邦类型逐一判定） | XML修饰器（城邦类型→人口×6条） |
| Vytautas | 中世纪 | 指定城市每回合 +8 忠诚，并创建1个带免费晋升的骑士单位；2 次使用次数 | XML修饰器（忠诚+赠单位），ActionCharges=2 |
| Akbar | 文艺复兴 | 任意政体 +1 万能政策槽 | XML修饰器（政策槽） |
| Askia | 文艺复兴 | 征服的拥有纪念碑的城市给予1份"Cowrie（贝币）"专属奢侈品（+4 宜居度）；劫掠区域收益翻倍（永久） | XML修饰器（专属资源+劫掠×2） |
| Isabella I | 文艺复兴 | 赠予1个免费大探险家（JNR联动）；商人单位 +2 视野，海军单位击杀敌人时产生大探险家点数〔替代版：每座圣地建筑 +1 大探险家点/回合〕 | XML修饰器（JNR联动+单位加成×6条） |
| Ismail I | 文艺复兴 | 黑暗时代期间用骑兵单位攻下城市时将其转化为你的主流宗教（永久能力）；黄金时代期间艺术巨作基础文化产出翻倍 | XML修饰器+单位能力 |
| Julius II | 文艺复兴 | 给予 455 点奇观建造生产力 | XML修饰器（奇观锤） |
| Lorenzo the Magnificent | 文艺复兴 | 此城所有文艺复兴时代奇观增加 2 个艺术巨作槽（覆盖8座指定奇观）；黄金时代期间赠予1个免费大艺术家 | XML修饰器（奇观槽位×8条+条件赠伟人） |
| Louis XIV | 文艺复兴 | 所有政府广场建筑增加 3 个艺术巨作槽；放置其中的雕塑文化产出 ×3（永久） | XML修饰器（槽位×10条+巨作产出×10条） |
| Maria Theresa | 文艺复兴 | 城邦提供的每种独特改良（摩艾/那斯卡/卡霍基亚等9种）：所有城市 +20% 大艺术家点数、+20% 大音乐家点数/回合（永久） | XML修饰器（城邦改良→伟人点%×18条） |
| Skanderbeg | 文艺复兴 | 立即击杀2格范围内所有敌单位；你的2格范围内陆地战斗单位恢复全部移动力与攻击能力 | XML修饰器（范围杀伤+范围恢复） |
| Ulug Beg | 文艺复兴 | 每放置1个新学院区域时 +200 科技 | XML修饰器（区域放置触发科技） |
| Mehmet Ali | 工业 | 所有单位升级金币费用 -100%（免费升级）；赠予1项随机免费科技 | XML修饰器（升级折扣+随机科技） |
| Meiji | 工业 | 以工业区或社区替换农场时获得一笔金币；工业区与社区：每个相邻区域 +2 食物（永久） | XML修饰器（替换触发金币+邻接产出×4条） |
| Otto von Bismark | 工业 | 成为指定城邦的宗主国并移除其他所有玩家的使者；当前政体每张外交政策卡 +1 外交支持/回合（永久） | XML修饰器（城邦宗主+政策卡外交支持） |
| Prithvi Narayan Shah | 工业 | 所有近战与远程陆地单位 +3 战斗力；在外国大陆作战时额外 +3 战斗力（永久能力） | XML修饰器+单位能力×2 |
| Ataturk | 现代 | 给予 400 点生产力（可用于任何建造或单位训练）；3 次使用次数 | XML修饰器（通用锤），ActionCharges=3 |
| Haile Selassie | 现代 | +2 外交胜利点 | XML修饰器 |
| Lee Kuan Yew | 原子能 | 大商人使用次数 +1（永久）〔Tycoons 联动版追加：立即创建1个"Investor"单位〕 | XML修饰器（伟人次数；另有联动变体） |
| Zayed bin Sultan Al Nahyan | 原子能 | 你的城市每拥有1种不同的供电战略资源（煤/石油/铀），该城 +20% 金币（永久） | XML修饰器（资源→金%×3条） |
| Rainier III | 信息 | 你当前每多持有1份富余奢侈品，给予 200 旅游业绩；每座滨水区/游乐码头建筑为海滨度假村 +60% 旅游（最高+300%） | XML修饰器（奢侈份数旅游+建筑旅游%×5条） |

> 可选配置（默认关闭）：把原版拿破仑（+1万能政策槽）、古斯塔夫二世（+1军事政策槽）改列为大统治者。

---

## 5. AOM Equally Great Scientists 平等伟人科学家（1335152349）

实现方式：删除原版科学家后重建（Delete+Insert）；新增"科学巨作"（GreatWork of Science）对象类型；专属世界唯一建筑；UI 替换。科学巨作产出见各行。

### 新增大科学家（8 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Theophrastus | 古典 | 该学院区域的科技邻接加成同时提供等量食物（永久） | XML修饰器（邻接映射） |
| William of Ockham | 中世纪 | 创作科学巨作《Occam's Razor》（+2 科技、+1 信仰） | 科学巨作系统 |
| Fritz Haber | 现代 | 农场地块 +1 食物/回合（永久） | XML修饰器（改良产出） |
| Marie Curie | 现代 | 立即建成"镭研究所"——学院区专属唯一建筑：+3 科技、+2 生产力、+1 大科学家点/回合 | 专属建筑（依赖mod建筑） |
| Satyendra Nath Bose | 现代 | 创作科学巨作《Planck's Law and Hypothesis of Light Quanta》（+6 科技） | 科学巨作系统 |
| Wilhelm Röntgen | 现代 | 一次性获得 1140 科技 | XML修饰器（一次性科技，随速度缩放） |
| Stephen Hawking | 原子能 | 创作科学巨作《A Brief History of Time》（+4 科技、+3 文化） | 科学巨作系统 |
| Tim Berners-Lee | 信息 | 一次性获得 1850 科技 | XML修饰器（一次性科技，随速度缩放） |

### 修改的原版大科学家（17 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| 伽利略 Galileo | 文艺复兴 | 创作科学巨作《Galileo's Middle Finger》（+4 科技） | 科学巨作系统（替换原效果） |
| 牛顿 Newton | 文艺复兴 | 创作科学巨作《Principia》（+4 科技） | 科学巨作系统 |
| 达尔文 Darwin | 工业 | 创作科学巨作《The Origin of Species》（+5 科技） | 科学巨作系统 |
| 诺贝尔 Nobel | 现代 | 创作科学巨作《Nobel Prize》（+3 文化、+2 科技） | 科学巨作系统 |
| 图灵 Turing | 现代 | 创作科学巨作《The Chemical Basis of Morphogenesis》（+6 科技） | 科学巨作系统 |
| 爱因斯坦 Einstein | 现代 | 创作科学巨作《The Annus Mirabilis Papers》（+6 科技） | 科学巨作系统 |
| 薛定谔 Schrödinger | 原子能 | 创作科学巨作《Schrödinger's Cat》（+7 科技） | 科学巨作系统 |
| 萨根 Sagan | 信息 | 创作科学巨作《Voyager Record》（+8 文化） | 科学巨作系统 |
| 希帕提娅 Hypatia | 古典 | 创作科学巨作《Hypatia's Astrolabe》（+2 科技） | 科学巨作系统 |
| 扎哈拉维 al-Zahrawi | 中世纪 | 创作科学巨作《Kitab Al-tasrif》（+2 科技） | 科学巨作系统 |
| 欧几里得 Euclid | 古典 | 一次性获得 120 科技 | XML修饰器（一次性科技） |
| 海亚姆 Khayyam | 中世纪 | 一次性获得 150 科技；该学院区域的科技邻接加成同时提供等量文化（永久） | XML修饰器（一次性科技+邻接映射） |
| 杜夏特莱 du Chatelet | 文艺复兴 | 一次性获得 600 科技 | XML修饰器（一次性科技） |
| 克沃莱克 Kwolek | 信息 | 发明凯夫拉：所有单位 +10 防御战斗力（永久） | XML修饰器（全局防御） |
| 门捷列夫 Mendeleev | 工业 | 立即建成"门捷列夫度量衡研究所"——学院区专属唯一建筑：+5 科技、+1 大科学家点/回合 | 专属建筑 |
| 萨拉姆 Salam | 信息 | 立即建成"阿卜杜斯·萨拉姆国际理论物理中心"——学院区专属唯一建筑：+9 科技、+1 大科学家点/回合 | 专属建筑 |
| 阿耶波多 Aryabhata | 古典 | 立即建成"那兰陀大学"——学院区专属唯一建筑：+2 科技、+1 大科学家点/回合 | 专属建筑 |

---

## 6. AOM Equally Great Engineers 平等伟人工程师（1373931635）

实现方式：删原版重建；新增"工程巨作"对象类型；专属奇观/建筑；达·芬奇改类别为大艺术家；UI 替换。

### 新增大工程师（10 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Banū Mūsā | 中世纪 | 创作工程巨作《Book of Ingenious Devices》（+8 生产力） | 工程巨作系统 |
| Francesco di Giorgio | 文艺复兴 | 立即在此城建成的远古、中世纪、文艺复兴城墙 | XML修饰器（赠三级城墙） |
| Johannes Gutenberg | 文艺复兴 | 立即在工业区建成"古登堡工坊"——专属奇观：+3 信仰、+3 生产力 | 专属奇观（依赖mod奇观） |
| Frederick Olmsted | 工业 | 立即在市中心建成"中央公园"——专属奇观：+2 宜居度 | 专属奇观 |
| Isambard Brunel | 工业 | 立即在市中心建成"大西部铁路"——专属奇观：+2 文化、+6 生产力 | 专属奇观 |
| Alexander Fleming | 现代 | 单一城市立即 +3 人口 | XML修饰器（加人口） |
| Hedy Lamarr | 现代 | 发明"保密通信系统"：所有现代、原子能、信息时代的海军袭击者与海军远程单位 +5 战斗力（永久） | XML修饰器（单位战力） |
| Fazlur Rahman Khan | 原子能 | 该城市 +4 住房 | 原版修饰器 GREATPERSON_CITY_HOUSING_LARGE |
| Gurmukh Sarkaria | 原子能 | 立即在工业区建成"伊泰普水坝"——专属奇观：+20 生产力 | 专属奇观 |
| Mars Exploration Rover Team | 信息 | 太空竞赛项目 +100% 生产力（永久） | XML修饰器（项目锤%） |

### 修改的原版大工程师（4 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| 毕昇 Bi Sheng | 中世纪 | 该工业区的生产力邻接加成同时提供等量文化（永久） | XML修饰器（邻接映射） |
| 简·德鲁 Jane Drew | 原子能 | 该城市 +3 宜居度 | XML修饰器（宜居，Amount=3） |
| 罗布林 Roebling | 原子能 | 立即在市中心建成"布鲁克林大桥"——专属奇观：+4 文化、+4 金币 | 专属奇观 |
| 达·芬奇 Leonardo da Vinci | 文艺复兴 | **类别改为大艺术家**；创作3件艺术巨作：《Mona Lisa》《Salvator Mundi》《Lady with an Ermine》（各 +3 文化） | 改类别+艺术巨作（原工程师版删除） |

---

## 7. AOM Equally Great Merchants 平等伟人商人（1356636218）

实现方式：删原版重建；新增6种专属奢侈品+5座专属建筑；UI 替换。

### 新增大商人（11 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| Hippalus | 古典 | 给予 1 份"胡椒"专属奢侈品（+4 宜居度） | XML修饰器+专属资源 |
| Kanishka | 古典 | 商路容量 +1；赠予1个免费商人单位；+100 信仰 | 原版修饰器组合（商路容量+免费商人+FAITH_SMALL） |
| Dick Whittington | 中世纪 | 立即在市中心建成"惠廷顿学院"——专属建筑：+3 住房 | 专属建筑 |
| Ichtacka Pochteca | 中世纪 | 给予 1 份"阿兹特克绿松石"专属奢侈品（+4 宜居度） | XML修饰器+专属资源 |
| Joseph of Spain | 中世纪 | 给予 1 份"藏红花"专属奢侈品（+4 宜居度） | XML修饰器+专属资源 |
| James Lancaster | 文艺复兴 | 立即建成"东印度公司"——专属建筑：商路目的地每种奢侈品 +1 金币 | 专属建筑 |
| David Ogilvy | 现代 | 任意政体 +1 万能政策槽 | XML修饰器（政策槽） |
| David Sarnoff | 现代 | 立即建成"全国广播公司（NBC）"——专属奇观：+5 金币/回合，且为10格内任意市中心 +1 宜居度；广播塔为6格内每座城市 +1 宜居（永久） | 专属奇观+XML修饰器（建筑范围宜居） |
| Lizzie Magie | 现代 | 给予 2 份"桌面游戏"专属奢侈品（各 +4 宜居度） | XML修饰器+专属资源 |
| Raymond Rubicam | 原子能 | 该商业中心的金币邻接加成同时提供等量文化（永久）；另含商路容量 +1 与对有商路文明的旅游加成（原版修饰器） | XML修饰器（邻接映射）+原版修饰器 |
| Jeff Bezos | 信息 | 给予 2 份"电子书"奢侈品（各 +6 宜居度） | XML修饰器+专属资源 |

### 修改的原版大商人（5 位）

| 伟人 | 时代 | 完整效果 | 实现方式 |
|---|---|---|---|
| 美第奇 Medici | 文艺复兴 | 立即建成"美第奇银行"——专属建筑：+2 金币、+1 大商人点/回合，并带 2 个万能巨作槽 | 专属建筑 |
| 托达尔·马尔 Todar Mal | 文艺复兴 | 此城农场地块 +1 金币/回合（永久） | XML修饰器（单城改良产出） |
| 阿斯特 Astor | 工业 | 吞并相邻地块（10 次使用次数） | 原版修饰器 GREATPERSON_GRANT_PLOT，ActionCharges=10 |
| 布里德洛夫 Breedlove | 现代 | 给予 2 份"护发产品"专属奢侈品（各 +4 宜居度） | XML修饰器+专属资源 |
| 富格尔 Fugger | 文艺复兴 | 立即在此区域建成"富格莱"——专属建筑：+3 住房 | 专属建筑 |
