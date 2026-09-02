# 文明6 伟人 Mod 全景分析与移植蓝图

> 数据来源：压缩包内 7 个 mod 的完整解包解析（313 条伟人记录、513 条本地化文本）+ 文明6 Wiki 原版数据（风云变幻规则，含巴比伦包等 DLC 标注）。
> 用途：逐个伟人移植整合、替换原版效果、生成新 mod 的参考底稿。

---

## 一、7 个 Mod 总览

| Mod | 作者 | 性质 | 新增伟人 | 对原版的改动 | 冲突风险 |
|---|---|---|---|---|---|
| **Team PVP More GreatPeople 伟人补充包** (3497524344) | Nwflower（千川白浪） | 纯新增 | 66 位（将军10/科学家10/工程师10/商人8/作家23/音乐家5） | 不改原版伟人；可选配置改后期伟人价格 | 低，与任何mod兼容 |
| **Nyguita More Great People 更多伟人** (2559462758) | Nyguita | 纯新增 | 88 位（除先知外每类11位）+ 77件巨作 | 不改原版伟人 | 低-中（伟人池膨胀） |
| **Sumus Magnus Great People Expansion 伟人扩展** (2448605286) | Plati | 纯新增+联动 | ~70 位（将军16/统帅10/科学家14/工程师12/商人12/作家10，含可选开关）+ 建筑/资源/巨作 | 不改原版伟人 | 低-中 |
| **Great Sovereigns 大统治者伟人** (2973448849) | Plati | **新增类别** | 32 位大统治者 + 专属项目/政策卡/万神殿/资源/建筑 | 新增 GREAT_PERSON_CLASS_GreatSovereigns 类；可选把拿破仑、古斯塔夫改列为统治者 | 中（改政府广场、可选改阿尔罕布拉宫） |
| **Equally Great Scientists 平等伟人科学家** (1335152349) | AOM | **重平衡+替换** | 新增6位；重做全部24位原版科学家 | 删除原版科学家后重建；新增"科学巨作"系统；替换UI | 高（与一切改科学家的mod冲突） |
| **Equally Great Engineers 平等伟人工程师** (1373931635) | AOM | **重平衡+替换** | 新增10位；重做原版工程师 | 删重建原版工程师；达·芬奇改为大艺术家；新增"工程巨作"系统 | 高 |
| **Equally Great Merchants 平等伟人商人** (1356636218) | AOM | **重平衡+替换** | 新增11位；重做原版商人 | 删重建原版商人；新增6种奢侈品+5座专属建筑 | 高 |

**三类 mod 的本质区别（移植时至关重要）：**

1. **纯新增型**（Team PVP / Nyguita / Sumus Magnus）——只 INSERT 新行，不动原版数据。移植=抽取对应文件段即可，最安全。
2. **新类别型**（Great Sovereigns）——新增一整套类（class）、单位、项目、政策卡、产出类型。移植单个统治者需要连带移植整套基础设施，**不能**只拷单人。
3. **替换型**（AOM 平等三部曲）——先 `<Delete>` 原版伟人再重建，并替换 UI 文件。移植=直接替换原版同名伟人，正好契合你"替换原本伟人效果"的目标，但会破坏依赖原版伟人的其他mod。

---

## 二、原版伟人完整数据（风云变幻规则）

### 2.1 招募费用（标准速度）

| 时代 | 古典 | 中世纪 | 文艺复兴 | 工业 | 现代 | 原子能 | 信息 |
|---|---|---|---|---|---|---|---|
| 基准点数 | 60 | 120 | 240 | 420 | 660 | 960 | 1200 |

> 联机（双倍速）减半：30/60/90/180/270/420/600。Team PVP mod 的"降低成本"配置即把文艺复兴及以后压到联机速标准（180/360/540/840/1200，标准速换算）。大先知机制特殊：共享限量池（玩家人数一半+1），费用随被认领数量递增，可用信仰/金币补差价。

### 2.2 原版九类伟人名册

通用规则：所有伟人4移动力；大将军/大海军统帅自带"+5力+1移动力"光环（2格范围，同代及次代单位）；大作家2部作品、大艺术家3部、大音乐家2部；毛里无法招募大作家，刚果（姆本巴）无法招募大先知。

#### 大作家（29位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 荷马 Homer | 古典 | 《奥德赛》《伊利亚特》 |
| 跋娑 Bhasa | 古典 | 《Madhyama Vyayoga》《Pratima-nataka》 |
| 屈原 Qu Yuan | 古典 | 《楚辞》《哀郢》 |
| 奥维德 Ovid | 古典 | 《变形记》《女杰书简》 |
| 蚁垤 Valmiki | 古典 | 《罗摩衍那》《Yoga Vasistha》〔巴比伦包〕 |
| 乔叟 Chaucer | 中世纪 | 《坎特伯雷故事集》《Troilus and Criseyde》 |
| 李白 Li Bai | 中世纪 | 《月下独酌》《In the Mountains on a Summer Day》 |
| 紫式部 Murasaki Shikibu | 中世纪 | 《紫式部日记》《源氏物语》 |
| 鲁米 Rumi | 中世纪 | 《Divani Shamsi Tabriz》《玛斯纳维》〔巴比伦包〕 |
| 塞万提斯 Cervantes | 文艺复兴 | 《堂吉诃德》《训诫小说集》 |
| 莎士比亚 Shakespeare | 文艺复兴 | 《罗密欧与朱丽叶》《哈姆雷特》 |
| 马基雅维利 Machiavelli | 文艺复兴 | 《李维论》《君主论》 |
| 卡文迪许 Cavendish | 文艺复兴 | 《The Blazing World》《Observations upon Experimental Philosophy》 |
| 多诺瓦夫人 d'Aulnoy | 文艺复兴 | 《Fair Goldilocks》《The Dolphin》 |
| 简·奥斯汀 Jane Austen | 工业 | 《傲慢与偏见》《理智与情感》 |
| 爱伦·坡 Poe | 工业 | 《泄密的心》《乌鸦》 |
| 普希金 Pushkin | 工业 | 《叶甫盖尼·奥涅金》《鲍里斯·戈都诺夫》 |
| 歌德 Goethe | 工业 | 《浮士德》《少年维特的烦恼》 |
| 玛丽·雪莱 Mary Shelley | 工业 | 《弗兰肯斯坦》《最后的人》 |
| 乔伊斯 Joyce | 现代 | 《尤利西斯》《都柏林人》 |
| 狄金森 Dickinson | 现代 | 《A Bird Came Down the Walk》《Success is Counted Sweetest》 |
| 托尔斯泰 Tolstoy | 现代 | 《战争与和平》《安娜·卡列尼娜》 |
| 马克·吐温 Twain | 现代 | 《哈克贝利·费恩历险记》《汤姆·索亚历险记》 |
| 碧雅翠丝·波特 Potter | 现代 | 《彼得兔的故事》《The Tailor of Gloucester》〔巴比伦包〕 |
| 菲茨杰拉德 Fitzgerald | 现代 | 《人间天堂》《The Beautiful and the Damned》 |
| 泰戈尔 Tagore | 原子能 | 《家庭与世界》《园丁集》 |
| 威尔斯 H.G. Wells | 原子能 | 《世界大战》《时间机器》 |
| 恰佩克 Capek | 信息 | 《R.U.R》《鲵鱼之乱》 |
| 米斯特拉尔 Mistral | 信息 | 《Lecturas para mujeres》《死亡十四行诗》〔巴比伦包〕 |

#### 大艺术家（23位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 安德烈·卢布廖夫 Rublev | 文艺复兴 | 《受胎告知》《光荣救世主》《升天》（宗教×3） |
| 米开朗基罗 Michelangelo | 文艺复兴 | 《西斯廷天顶画》《哀悼基督》《大卫》 |
| 多纳泰罗 Donatello | 文艺复兴 | 《圣马可》《加塔梅拉塔骑马像》《朱迪斯斩荷罗孚尼》 |
| 博斯 Bosch | 文艺复兴 | 《人间乐园》《最后的审判》《干草车三联画》 |
| 贝赫扎德 Behzad | 文艺复兴 | 《帖木儿与埃及王之战》等3件〔巴比伦包〕 |
| 伦勃朗 Rembrandt | 工业 | 《Andries de Graeff》《Agatha Bas》《亚伯拉罕与以撒》 |
| 格列柯 El Greco | 工业 | 《三王来朝》《圣母升天》《托莱多风景》 |
| 仇英 Qiu Ying | 工业 | 《汉宫春晓图》《莲溪渔隐图》《赤壁图》 |
| 提香 Titian | 工业 | 《Assunta》《莎乐美》《查理五世骑马像》 |
| 长谷川等伯 Tōhaku | 工业 | 《松林图》《枫树图》《花鸟图》〔巴比伦包〕 |
| 张承业 Jang Seung-eop | 现代 | 3件风景画 |
| 安圭索拉 Anguissola | 现代 | 3件肖像画 |
| 考夫曼 Kauffman | 现代 | 3件肖像画 |
| 葛饰北斋 Hokusai | 现代 | 《神奈川冲浪里》《诹访湖》《凯风快晴》 |
| 埃德莫尼亚·刘易斯 Lewis | 原子能 | 3件雕塑 |
| 莫奈 Monet | 原子能 | 《睡莲》《印象·日出》《干草堆》 |
| 科洛 Collot | 原子能 | 3件雕塑 |
| 梵高 Van Gogh | 原子能 | 《星月夜》《夜间咖啡馆露台》《夜间咖啡馆》 |
| 阿姆丽塔·谢尔-吉尔 Sher-Gil | 信息 | 3件肖像 |
| 奥尔洛夫斯基 Orlovsky | 信息 | 3件雕塑 |
| 克里姆特 Klimt | 信息 | 《吻》等3件 |
| 玛丽·卡萨特 Cassatt | 信息 | 3件肖像 |
| 康定斯基 Kandinsky | 信息 | 3件〔巴比伦包〕 |

#### 大音乐家（18位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 贝多芬 Beethoven | 工业 | 《欢乐颂》《英雄交响曲》 |
| 巴赫 Bach | 工业 | 《G小调小赋格》《无伴奏大提琴组曲》 |
| 八桥检校 Yatsuhashi Kengyo | 工业 | 《六段之调》《八段之调》 |
| 维瓦尔第 Vivaldi | 工业 | 《四季·冬》《La Notte协奏曲》 |
| 莫扎特 Mozart | 工业 | 《小夜曲》《第40交响曲》 |
| 康特米尔 Cantemir | 工业 | 3部作品〔巴比伦包〕 |
| 李斯特 Liszt | 现代 | 《超技练习曲No.9》《乡村客栈之舞》 |
| 柴可夫斯基 Tchaikovsky | 现代 | 《1812序曲》《小天鹅之舞》 |
| 戈麦斯 Gomes | 现代 | 《Fosca》《Alvorada》 |
| 刘天华 Liu Tianhua | 现代 | 《良宵》《空山鸟语》 |
| 肖邦 Chopin | 现代 | 《降E大调夜曲》《辉煌大圆舞曲》 |
| 乔普林 Joplin | 现代 | 3部作品〔巴比伦包〕 |
| 罗萨斯 Rosas | 原子能 | 《Sobre las Olas》《Vals Carmen》 |
| 德沃夏克 Dvořák | 原子能 | 《自新大陆》《小夜曲No.22》 |
| 利留卡拉尼 Lili'uokalani | 原子能 | 《利留卡拉尼的祈祷》《Sanoe》 |
| 克拉拉·舒曼 Schumann | 原子能 | 《前奏曲与赋格》《Toccatina》 |
| 列昂托维奇 Leontovych | 信息 | 《钟声颂歌》《合唱团前奏曲》 |
| 高哈尔·简 Gauhar Jaan | 信息 | 两首拉格 |

#### 大工程师（21位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 伊姆霍特普 Imhotep | 中世纪 | 奇观+175锤，远古/古典奇观翻倍（2次）〔巴比伦包〕 |
| 毕昇 Bi Sheng | 中世纪 | 城市区域位+1；触发印刷术尤里卡 |
| 米利都的伊西多尔 Isidore | 中世纪 | 奇观+215锤（2次） |
| 圣乔治的詹姆斯 James of St. George | 中世纪 | 立即建成远古+中世纪城墙（3次） |
| 布鲁内莱斯基 Brunelleschi | 文艺复兴 | 奇观+315锤（2次） |
| 达·芬奇 Leonardo da Vinci | 文艺复兴 | 随机现代科技尤里卡；工坊+3文化 |
| 希南 Mimar Sinan | 文艺复兴 | 城市+1住房+1宜居；R&F：完成工业区时文化炸弹 |
| 阿达·洛芙莱斯 Ada Lovelace | 工业 | 城市区域位+1；触发计算机尤里卡 |
| 埃菲尔 Eiffel | 工业 | 奇观+480锤（2次） |
| 詹姆斯·瓦特 James Watt | 工业 | 立即建成工坊+工厂；工厂+2锤 |
| 沙贾汗 Shah Jahan | 现代 | 国库一半转化为奇观锤，扣除2倍金币〔巴比伦包〕 |
| 阿尔托 Aalto | 现代 | 城市所有地块+1魅力 |
| 戈达德 Goddard | 现代 | 触发火箭学尤里卡；太空项目+20%锤 |
| 特斯拉 Tesla | 现代 | 区域建筑+2锤，覆盖范围+3格 |
| 简·德鲁 Jane Drew | 原子能 | 城市+4住房+3宜居 |
| 罗布林 Roebling | 原子能 | 城市+2住房+1宜居（2次） |
| 科罗廖夫 Korolev | 原子能 | 太空竞赛项目+1500锤 |
| 帕克斯顿 Paxton | 信息 | 娱乐中心区域建筑+1宜居，范围+3格 |
| 柯里亚 Correa | 信息 | 城市所有地块+2魅力 |
| 冯·布劳恩 von Braun | 信息 | 太空项目+100%锤 |
| 丹下健三 Kenzo Tange | 信息 | 城市每个区域提供邻接加成等值旅游〔巴比伦包〕 |

#### 大商人（24位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 科拉乌斯 Colaeus | 古典 | +100信仰；复制该地块奢侈品至首都 |
| 克拉苏 Crassus | 古典 | +60金；吞并相邻地块（3次） |
| 张骞 Zhang Qian | 古典 | +1商路容量；通此城外国商路双方+2金 |
| 伊本·法德兰 Ibn Fadlan | 中世纪 | +1商路容量；通城邦商路+2信仰〔巴比伦包〕 |
| 雅典的伊琳娜 Irene | 中世纪 | +1商路容量+复制奢侈品；R&F：+1总督头衔 |
| 马可·波罗 Marco Polo | 中世纪 | 免费商人单位+1商路容量；通此城外国商路双方+2金 |
| 巴尔迪 Bardi | 中世纪 | +200金+1使者 |
| 周达观 Zhou Daguan | 文艺复兴 | 在城邦获得3使者〔巴比伦包〕 |
| 美第奇 Medici | 文艺复兴 | 立即建成市场+银行；银行+2万能巨作槽 |
| 富格尔 Fugger | 文艺复兴 | +200金+2使者 |
| 托达尔·马尔 Todar Mal | 文艺复兴 | +1使者；国内商路按目的地区域数+金 |
| 亚当·斯密 Adam Smith | 工业 | +1经济政策槽；R&F：+500金+1总督头衔 |
| 阿斯特 Astor | 工业 | +500金+2使者 |
| 斯皮尔斯伯里 Spilsbury | 工业 | 创造"玩具"奢侈品（+4宜居） |
| 莱佛士 Raffles | 现代 | 吞并城邦且该城+10忠诚〔巴比伦包〕 |
| 洛克菲勒 Rockefeller | 现代 | +1石油/商路按战略资源+金；GS：每回合+3石油 |
| 布里德洛夫 Breedlove | 现代 | 对有商路文明+25%旅游 |
| 戈达德 Goddard | 现代 | 对全部文明外交能见度+1 |
| 鲁宾斯坦 Rubinstein | 原子能 | 2份"化妆品"（各+4宜居） |
| 李维·斯特劳斯 Strauss | 原子能 | 2份"牛仔裤"（各+4宜居） |
| 本茨 Bentz | 原子能 | +1商路容量；对有商路文明+25%旅游 |
| 雅诗·兰黛 Lauder | 信息 | 2份"香水"（各+6宜居） |
| 塔塔 Tata | 信息 | 学院区域+10旅游 |
| 岩隈久示 Ibuka | 信息 | 工业区+10旅游 |

#### 大科学家（24位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 张衡 Zhang Heng | 古典 | 天文导航/数学/工程学尤里卡（已触发则完成）〔巴比伦包〕 |
| 阿耶波多 Aryabhata | 古典 | 3个古典/中世纪随机科技尤里卡 |
| 欧几里得 Euclid | 古典 | 数学+1个中世纪随机科技尤里卡 |
| 希帕提娅 Hypatia | 古典 | 图书馆+1科技；立即建成图书馆 |
| 扎哈拉维 al-Zahrawi | 中世纪 | 1个中世纪/文艺复兴尤里卡；被动1格+20治疗 |
| 宾根的希尔德加德 Hildegard | 中世纪 | +100信仰；圣地邻接转科技 |
| 海亚姆 Khayyam | 中世纪 | 2个科技尤里卡+1个市政鼓舞 |
| 伊本·赫勒敦 Ibn Khaldun | 文艺复兴 | 学院+2住房+1宜居；幸福度非食物收益+40%〔巴比伦包〕 |
| 杜夏特莱 du Chatelet | 文艺复兴 | 3个文艺复兴/工业尤里卡 |
| 伽利略 Galileo | 文艺复兴 | 每相邻山脉+250科技 |
| 牛顿 Newton | 文艺复兴 | 立即建成图书馆+大学；大学+2科技 |
| 达尔文 Darwin | 工业 | 每相邻自然奇观+500科技 |
| 门捷列夫 Mendeleev | 工业 | 化学+1个工业随机尤里卡 |
| 詹姆斯·杨 James Young | 工业 | 2个工业/现代尤里卡；揭示石油 |
| 图灵 Turing | 现代 | 计算机+1个现代随机尤里卡 |
| 爱因斯坦 Einstein | 现代 | 1个现代尤里卡；研究实验室+4科技 |
| 诺贝尔 Nobel | 现代 | 1个现代/原子能尤里卡；+100点当前及未来伟人点数 |
| 薛定谔 Schrödinger | 原子能 | 3个原子能/信息尤里卡 |
| 阿马尔 Ammal | 原子能 | 每相邻雨林+400科技 |
| 利基 Leakey | 原子能 | 城市每件文物+350科技；文物300%旅游 |
| 米德 Mead | 原子能 | +1000科技+1000文化〔巴比伦包〕 |
| 萨根 Sagan | 信息 | 太空项目+3000锤 |
| 克沃莱克 Kwolek | 信息 | 太空项目+100%锤 |
| 萨拉姆 Salam | 信息 | 触发信息时代全部尤里卡 |

#### 大将军（24位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 布狄卡 Boudica | 古典 | 转换相邻蛮族单位 |
| 汉尼拔 Hannibal | 古典 | 1个陆军单位+1晋升 |
| 孙子 Sun Tzu | 古典 | 产生巨作《孙子兵法》 |
| 征侧 Trưng Trắc | 古典 | 永久-25%战争厌倦〔巴比伦包〕 |
| 埃塞尔弗莱德 Æthelflæd | 中世纪 | 立即创建骑士；R&F：城市+2忠诚/回合 |
| 熙德 El Cid | 中世纪 | 陆军单位编成军团 |
| 成吉思汗/帖木儿 Genghis/Timur | 中世纪 | +1晋升+25%经验（R&F帖木儿替换成吉思汗） |
| 恩津加/阿米娜 Nzinga/Amina | 文艺复兴 | +1使者（大谈判家包阿米娜替换恩津加） |
| 古斯塔夫二世 Gustavus | 文艺复兴 | 创建带1晋升射石炮 |
| 圣女贞德 Jeanne d'Arc | 文艺复兴 | 产生1件圣物 |
| 丹达拉 Dandara | 工业 | 授予带1晋升武僧（2次）〔巴比伦包〕 |
| 玻利瓦尔/圣马丁 Bolívar/San Martín | 工业 | +2使者（玛雅包圣马丁替换） |
| 拿破仑 Napoleon | 工业 | 陆军单位编成军队 |
| 章西女王 Lakshmibai | 工业 | 创建带1晋升骑兵 |
| 图帕克·阿马鲁 Tupac Amaru | 现代 | 敌境每无防区域生成火枪手〔巴比伦包〕 |
| 莫纳什 Monash | 现代 | +1晋升+75%经验 |
| 拉斯科娃 Raskova | 现代 | 航空港空中槽位+1 |
| 萨摩里·杜尔 Touré | 现代 | 创建带1晋升步兵（R&F：特种部队） |
| 麦克阿瑟 MacArthur | 原子能 | 创建带1晋升坦克；GS：+1石油/回合 |
| 艾森豪威尔 Eisenhower | 原子能 | 军事单位+5%锤 |
| 朱可夫 Zhukov | 原子能 | 陆军夹击加成+50% |
| 苏迪曼 Sudirman | 原子能 | +1晋升+100%经验；R&F：城市+6忠诚 |
| 马苏德 Massoud | 信息 | 创建带1晋升现代反坦克 |
| 维马拉拉特纳 Wimalaratne | 信息 | +1晋升+100%经验 |

#### 大海军统帅（23位）

| 伟人 | 时代 | 效果/作品 |
|---|---|---|
| 阿尔忒弥西亚 Artemisia | 古典 | 海军单位+1晋升 |
| 杜伊利乌斯 Duilius | 古典 | 海军单位编成舰队 |
| 地米斯托克利 Themistocles | 古典 | 创建四段战船；GS：海军远程+20%锤 |
| 航海家汉诺 Hanno | 古典 | 海军近战+2移动力〔巴比伦包〕 |
| 希墨里奥斯 Himerios | 中世纪 | +1晋升+25%经验〔巴比伦包〕 |
| 莱夫·埃里克松 Erikson | 中世纪 | 海军可进海洋格；GS：+1视野 |
| 拉金德拉·朱罗 Chola | 中世纪 | 劫掠收益+40%；GS：海军+3力 |
| 郑和 Zheng He | 中世纪 | +1使者；GS：免费商队+商路容量+1 |
| 德雷克 Drake | 文艺复兴 | +75金+劫掠商路+50%；GS：创建私掠船 |
| 圣克鲁斯 Santa Cruz | 文艺复兴 | 编成无敌舰队 |
| 李舜臣 Yi Sun-Sin | 文艺复兴 | 创建铁甲舰；GS：+1煤/回合 |
| 麦哲伦 Magellan | 文艺复兴 | +300金+复制奢侈品〔需R&F〕 |
| 郑一嫂 Ching Shih | 工业 | +100金+劫掠+60%；GS：+500金 |
| 纳尔逊 Nelson | 工业 | 海军夹击+50%；GS：立即建成灯塔+造船厂 |
| 布布利娜 Bouboulina | 工业 | +1晋升+50%经验 |
| 马修·佩里 Perry | 现代 | 成为城邦宗主国〔巴比伦包〕 |
| 希佩尔 Hipper | 现代 | 创建战列舰；GS：+1煤/回合 |
| 利斯博阿 Lisboa | 现代 | -25%战争厌倦 |
| 东乡平八郎 Togo | 现代 | +1晋升+75%经验；R&F：+6忠诚 |
| 尼米兹 Nimitz | 原子能 | 海军袭击者+20%锤；GS：创建潜艇+1石油/回合 |
| 霍珀 Hopper | 原子能 | 随机解锁2个免费科技（GS） |
| 戈尔什科夫 Gorshkov | 原子能 | +1晋升+100%经验 |
| 费尔南多 Fernando | 信息 | +1晋升+200%经验 |

#### 大先知（16位，机制特殊）

| 时代 | 人物 |
|---|---|
| 古典 | 孔子、施洗约翰、老子、释迦牟尼、西门·彼得、琐罗亚斯德 |
| 中世纪 | 阿迪·商羯罗、菩提达摩、爱任纽、太安万侣、松赞干布 |
| 文艺复兴 | Haji Huud、Madhva Acharya、马丁·路德、托马斯·阿奎那、阿西西的方济各 |

> 所有大先知效果相同：在圣地/巨石阵创立宗教。工业时代起无法招募。**三个新增型mod都没有新增大先知**，这是一个完全空白的扩展位。

---

## 三、Mod 伟人完整清单

### 3.1 Team PVP伟人补充包（66条记录）

**大将军（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 卫青 | 古典 | 创建1个拥有+2  移动力的陆军近战单位。 |
| 霍去病 | 古典 | 赠予军事陆军单位1次强化等级。 |
| 岳飞 | 中世纪 | 创建1个拥有+2  移动力的抗骑兵单位。 |
| 贝利撒留 | 中世纪 | 创建1个拥有+1  移动力的轻骑兵单位。 |
| 戚继光 | 文艺复兴 | 立即创建拥有1次升级的火枪手单位，每回合提供1点  硝石。 |
| 李自成 | 文艺复兴 | 把一个军事陆地单位变成军团。 |
| 罗伯特・李 | 工业 | 为骑兵单位+10% Production 生产力。 |
| 老毛奇 | 工业 | 所有陆地单位+30%支援加成。 |
| 卡特利特·马歇尔 | 现代 | 立即创建拥有1次升级的大炮单位，每回合提供1点  石油。 |
| 托马斯・布莱梅 | 现代 | 所有陆地单位+1 Strength 战斗力。 |

**大科学家（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 刘徽 | 古典 | 在指定位置创作《九章算术》（ GreatWork_Writing 著作，提供 4 Science 科技值、4 Tourism 旅游业绩） |
| 祖冲之 | 古典 | 为机械和1个随机中世纪科技启动 TechBoosted 尤里卡时刻。 |
| 花拉子米 | 中世纪 | 在学院上激活。该学院的 Science 科技值相邻加成也提供 Production 生产力。 |
| 贾思勰 | 中世纪 | TechBoosted 尤里卡提供额外2%进度。 |
| 开普勒 | 文艺复兴 | 为所有文艺复兴时期的科技启动 TechBoosted 尤里卡时刻。 |
| 李时珍 | 文艺复兴 | 为卫生设备启动 TechBoosted 尤里卡时刻，获得1个医疗兵。 |
| 莫尔斯 | 工业 | 获得当前回合产出的等额 Science 科技值。 |
| 萨弗里 | 工业 | 为工业化启动 TechBoosted 尤里卡时刻，若已有 TechBoosted 尤里卡则解锁工业化科技。 |
| 居里夫人 | 现代 | 忽视普通科技要求，显示 RESOURCE_URANIUM 铀。所有战略资源改良设施每回合额外产出1个对应资源。 |
| 贝尔 | 现代 | 为无线电启动 TechBoosted 尤里卡时刻。若已有 TechBoosted 尤里卡则解锁无线电科技。 |

**大工程师（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 李冰 | 古典 | 为城市提供 PRODUCTION 5点生产力（联机速度下），如果城市正在修建水利区域（水渠、运河或堤坝）则可以立即完成。 |
| 维特鲁威 | 古典 | 赠予1个免费的建造者单位，该城市建造奇观时+10% PRODUCTION 生产力。 |
| 宇文恺 | 中世纪 | 立即建造一个工作坊，该城市建造区域时+15% PRODUCTION 生产力。 |
| 苏颂 | 中世纪 | 立即建造一个水磨，该城市+5% PRODUCTION 生产力。 |
| 约瑟夫·帕克斯顿 | 文艺复兴 | 此城和所有相邻奇观的市中心+1 Amenities 宜居度。 |
| 蒯祥 | 文艺复兴 | 立即推进当前在建奇观25%的建造进度，文艺复兴及之前的奇观翻倍。此城所有世界奇观+2 CULTURE 文化值。 |
| 詹天佑 | 工业 | 在非首都市中心激活时，建造一条目标城市到首都的铁路。所有工业区+1 PRODUCTION 生产力相邻加成。 |
| 迈克尔·法拉第 | 工业 | 为所有城市提供15回合的清洁 POWER 电力供给。 |
| 托马斯·爱迪生 | 现代 | 拥有充足 POWER 电力供给的城市 +15% 项目 PRODUCTION 生产力，为1项工业时代及之后的随机科技启动尤里卡时刻。 |
| 茅以升 | 现代 | 为奇观提供225点 PRODUCTION 生产力（联机速度下），若为水上奇观则立即完成。所有单位无视河流的移动力减益。 |

**大商人（8位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 吕不韦 | 古典 | 立即建造一个市场，市场+1 GOLD 金币。 |
| 子贡 | 古典 | 所有贸易路线+1 GOLD 金币。 |
| 王玄策 | 中世纪 | 己方领土内或靠近己方领土的商人单位免遭掠夺。 |
| 裴明礼 | 中世纪 | +1 TradeRoute 贸易路线容量，+1 ENVOY 使者。 |
| 沈万三 | 文艺复兴 | 从现在起，每回合将获得等同于国库2%的 GOLD 金币。（上限1000） |
| 科西莫・梅第奇 | 文艺复兴 | 在选定的奢侈品单元格上激活，赠予一份该奢侈品给您的首都。该奢侈品将重复提供宜居度。 |
| 安德鲁・卡内基 | 工业 | +1 TradeRoute 贸易路线容量。改良后的 RESOURCE_IRON 铁资源+3 GOLD 金币。 |
| 顾维钧 | 工业 | 在城邦领土内激活。为玩家提供该城邦的宗主国能力。 |

**大作家（23位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 司马相如 | 古典 | — |
| 宋玉 | 古典 | — |
| 班固 | 古典 | — |
| 谢灵运 | 古典 | — |
| 杜甫 | 中世纪 | — |
| 白居易 | 中世纪 | — |
| 苏轼 | 中世纪 | — |
| 辛弃疾 | 中世纪 | — |
| 吴承恩 | 文艺复兴 | — |
| 施耐庵 | 文艺复兴 | — |
| 曹雪芹 | 文艺复兴 | — |
| 罗贯中 | 文艺复兴 | — |
| 托尔斯泰 | 工业 | — |
| 梁启超 | 工业 | — |
| 雨果 | 工业 | — |
| 海明威 | 现代 | — |
| 茅盾 | 现代 | — |
| 鲁迅 | 现代 | — |
| 沈从文 | 原子能 | — |
| 老舍 | 原子能 | — |
| 刘慈欣 | 信息 | — |
| 江南 | 信息 | — |
| 莫言 | 信息 | — |

**大音乐家（5位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 阿里斯托芬 | 古典 | — |
| 沃尔夫拉姆 | 中世纪 | — |
| 纪尧姆・德・马肖 | 中世纪 | — |
| 克劳迪奥·蒙特威尔第 | 文艺复兴 | — |
| 杜阿尔特·罗博 | 文艺复兴 | — |


### 3.2 Nyguita更多伟人（88条记录）

**大将军（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Eumenes of Cardia | 古典 | — |
| Zhuge Liang | 古典 | Trigger the TechBoosted Eureka for Military Tactics. If it is already triggered, instead… |
| Jan Žižka | 中世纪 | +5 Strength Combat Strength for all land units when defending. |
| Roger de Flor | 中世纪 | 10% Discount on Gold Gold and Faith Faith purchases when buying land military units in c… |
| Tomoe Gozen | 中世纪 | Instantly creates a Courser unit with 1 promotion level. |
| Albrecht von Wallenstein | 文艺复兴 | — |
| Federico da Montefeltro | 文艺复兴 | +1 Science Science from each GreatWork_Writing Great Work of Writing. +1 Culture Culture… |
| Hernán Cortés | 文艺复兴 | Instantly creates a Conquistador unit with 1 promotion level. |
| Geronimo | 工业 | +5 Strength Combat Strength when fighting ennemies with a higher base Strength Combat St… |
| Hijikata Toshizō | 工业 | Grants +4 Loyalty per turn for this city. |
| Emiliano Zapata | 现代 | Yields gained from pillaging are doubled. |

**大海军统帅（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Grace O'Malley | 文艺复兴 | Gain {Amount} Gold Gold. +75% rewards from Coastal Raids. |
| Hasekura Tsunenaga | 文艺复兴 | TradeRoute Trade Routes to more advanced civilizations grant +1 Science Science for ever… |
| Michiel de Ruyter | 文艺复兴 | +7 Strength Combat Strength for a naval unit. |
| Peter Tordenskjold | 文艺复兴 | Naval units have +5 Strength Combat Strength vs. district defenses. |
| Túpac Yupanqui | 文艺复兴 | — |
| Vasco da Gama | 文艺复兴 | Provides 2 Copies of RESOURCE_SPICES Spices. TradeRoute Trade Routes provides +50% Gold … |
| David Farragut | 工业 | Grants +4 Loyalty per turn for this city. |
| Fernando Villaamil | 工业 | Instantly creates a Destroyer. Grants 1 RESOURCE_OIL Oil per turn. |
| James Cook | 工业 | +2 Science Science, Culture Culture, and Gold Gold from each city-state you are Suzerain… |
| Pavlos Kountouriotis | 现代 | — |
| Jacques-Yves Cousteau | 原子能 | Gains {Amount} Culture. Reefs provides +2 Culture Culture. |

**大科学家（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Hippocrates | 古典 | Chosen city gains 1 Housing Housing. Increases growth by 5% in all cities. |
| Sun Simiao | 古典 | Reveals RESOURCE_NITER Niter without the normal technology requirement. |
| Roger Bacon | 中世纪 | Trigger the TechBoosted Eureka for Scientific Theory. If the Eureka for Scientific Theor… |
| Gerardus Mercator | 文艺复兴 | Naval and Embarked units gains +1 Movement Movement. Trigger the TechBoosted Eureka for … |
| Paracelsus von Hohenheim | 文艺复兴 | Universities provides +2 Food Food, +2 Gold Gold and +1 Housing Housing. |
| Ulugh Beg | 文艺复兴 | Palace and buildings in the Government Plaza and the Diplomatic Quarter provides +3 Scie… |
| John Muir | 工业 | Breathtaking tiles receive +1 SCIENCE Science and +1 CULTURE Culture. Grants a Naturalis… |
| Auguste Piccard | 现代 | Trigger the TechBoosted Eurekas for Flight and Advanced Flight. If the Eureka for Flight… |
| Edith Clarke | 现代 | Powered cities provides +{Amount}% Science Science |
| Jagadish Chandra Bose | 现代 | Trigger the TechBoosted Eurekas for Radio and Telecommunications. If the Eurekas for Rad… |
| Rachel Carson | 原子能 | Gain {Amount} Science Science for each Coast tile here or adjacent. + Gain {Amount} Cult… |

**大工程师（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Archimedes | 中世纪 | This city has an additional Ranged Ranged strike per turn. Instantly creates a Trebuchet. |
| Master Gerhard | 中世纪 | Grants {Amount} Production Production towards wonder construction. Wonders provides +3 F… |
| Sergius Orata | 中世纪 | — |
| Bartolomeo Cristofori | 文艺复兴 | Workshops provide +1 GreatMusician Great Musician point and have a GreatWork_Music Great… |
| Orbán | 文艺复兴 | +15% Production Production toward Siege units. Siege units gain +5 Strength Combat Stren… |
| Henry Bessemer | 工业 | Trigger the TechBoosted Eureka for Steel. If the Eureka for Steel has already been trigg… |
| Joseph-Marie Jacquard | 工业 | Instantly builds a Workshop and a Factory. This city have +2 Power Power. |
| Norbert Rillieux | 工业 | Plantations provides +2 Food Food, +2 Gold Gold and +1 Production Production. |
| Hugo Eckener | 现代 | Aircrafts have +1 Movement Movement and +1 Range Range |
| Sakichi Toyoda | 现代 | DISTRICT_INDUSTRIAL_ZONE Industrials Zones' adjacency bonuses gain an additional Science… |
| Nikolay Dollezhal | 原子能 | Grants 1 RESOURCE_URANIUM Uranium per turn. +25% Production towards nuclear projects. |

**大商人（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Gaius Maecenas | 古典 | Patronage of Great People costs 10% less Gold Gold. |
| Wang Anshi | 中世纪 | +1 Economic policy slot |
| Antonio Van Diemen | 文艺复兴 | International TradeRoute Trade Routes on foreign continents provides +1 Food Food, +1 Pr… |
| Jerome Horsey | 文艺复兴 | +1 Diplomatic policy slot |
| Pierre-Esprit Radisson | 文艺复兴 | Creates one copy of RESOURCE_NYGUITA_BEAVER Beaver, which provides +2 Amenities Amenitie… |
| Samuel de Champlain | 文艺复兴 | Instantly creates a Settler and a Musketman. |
| Elizabeth Macarthur | 工业 | Pastures trigger a culture bomb and provides +2 Gold Gold. |
| Ninomiya Sontoku | 工业 | Farms and Terrace Farms provides +1 Gold Gold. Cities with an established Governor recei… |
| Thomas Cook | 工业 | +50% Tourism Tourism from DISTRICT_WONDER Wonders, Sea Side Resorts and Ski Resorts |
| Solomon R. Guggenheim | 现代 | Gain {Amount} Gold Gold for every GreatWork_ReligiousGreatWork_SculptureGreatWork_Portra… |
| Satoru Iwata | 信息 | Research Labs provides +3 Culture Culture, +2 Gold Gold but -1 Science Science. Commerci… |

**大作家（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Lucian | 古典 | — |
| Al-Hariri of Basra | 中世纪 | — |
| Chrétien de Troyes | 中世纪 | — |
| Christine de Pizan | 文艺复兴 | — |
| Jules Verne | 工业 | — |
| Victor Hugo | 工业 | — |
| Jorge Luis Borges | 现代 | — |
| Osamu Dazai | 现代 | — |
| Sir Arthur Conan Doyle | 现代 | — |
| Umberto Eco | 原子能 | — |
| Kinoko Nasu | 信息 | — |

**大艺术家（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Giuseppe Arcimboldo | 文艺复兴 | — |
| Nicolas Poussin | 文艺复兴 | — |
| Antonio Canova | 工业 | — |
| Edgar Degas | 工业 | — |
| Katsushika Ōi | 工业 | — |
| Alphonse Mucha | 现代 | — |
| Amedeo Mogigliani | 现代 | — |
| Camille Claudel | 现代 | — |
| Jean-Michel Basquiat | 原子能 | — |
| Salvador Dalí | 原子能 | — |
| Peter Doig | 信息 | — |

**大音乐家（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Barbara Strozzi | 文艺复兴 | — |
| Richard Wagner | 工业 | — |
| Giacomo Puccini | 现代 | — |
| Ulvi Cemal Erkin | 现代 | — |
| Benjamin Britten | 原子能 | — |
| Iannis Xenakis | 原子能 | — |
| Louis W. Ballard | 原子能 | — |
| Olivier Messiaen | 原子能 | — |
| Steve Reich | 原子能 | — |
| Georg Friedrich Haas | 信息 | — |
| Yūgo Kanno | 信息 | — |


### 3.3 Sumus Magnus伟人扩展（72条记录）

**大将军（16位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Baibars | 中世纪 | Units have 20% less Strength Combat Strength reduction from being injured. |
| Gajah Mada | 中世纪 | Grants one copy of RESOURCE_PEPPER Pepper to this City. If the City is conquered, also g… |
| Hugues de Payens | 中世纪 | Unlocks and builds TEXTICON_TEMPALR_VAULT Templar Vault - a unique building that grants … |
| Jan Žižka | 中世纪 | Land units gain +4 Strength Combat Strength when fighting units with a higher base Stren… |
| Khalid ibn al-Walid | 中世纪 | Gain 200 Faith Faith. |
| Rurik | 中世纪 | Instantly creates a Settler and a Berserker. |
| Carolus Rex | 文艺复兴 | Allows the training of Caroleans (Requires Metal Casting). |
| Catherina Sforza | 文艺复兴 | Gain 300 Culture Culture. |
| Hernán Cortés | 文艺复兴 | Creates a Conquistador unit with one promotion. |
| Stanisław Żółkiewski | 文艺复兴 | Allows the training of Winged Hussars (Requires Mercantilism). |
| Giuseppe Garibaldi | 工业 | Melee units gain +3 Strength Combat Strength when fighting on your Capital Capital's hom… |
| Lawrence of Arabia | 现代 | Liberating a City grants +20% Culture in all cities for 10 turns. |
| Roman von Ungern-Sternberg | 现代 | Instantly creates five Keshigs. |
| Ulysses S. Grant | 现代 | +1 Diplomatic Victory point. |
| William Lendrum Mitchell | 现代 | Aerodromes and their buildings grants a free copy of air fighter unit when built. These … |
| Carl Gustaf Emil Mannerheim | 原子能 | All land units gain +4 Strength Combat Strength when defending. |

**大海军统帅（8位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Agrippa | 古典 | Grants 245 Production Production towards Wonder construction. |
| Ragnar Lodbrok | 中世纪 | Yields gained from pillaging are doubled for pillaging improvements. |
| Roger of Lauria | 中世纪 | Naval melee units gain +1 Strength Combat strength per unused Movement Movement. |
| Afonso de Albuquerque | 文艺复兴 | Grants one copy of RESOURCE_NUTMEG Nutmeg to this City if it is built on Capital Non-Cap… |
| Andrea Doria | 文艺复兴 | Naval melee units, upon conquest, convert cities to your majority religion. |
| Hayreddin Barbarossa | 文艺复兴 | Allows the training of Barbary Corsairs (Requires Medieval Faires). |
| Henry Morgan | 文艺复兴 | Grants 1 GOVERNOR Governor Title or recruits a new Governor. |
| Michiel de Ruyter | 文艺复兴 | Chosen city gains additional Ranged Attack per turn. |

**大科学家（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Aristotle | 古典 | Grants a free Wild Card Policy slot in any Government. |
| Cai Lun | 古典 | Unlocks and builds TEXTICON_PAPER_MAKER Paper Maker - a unique building that yields +1 S… |
| Averroes | 中世纪 | During GLORY_GOLDEN_AGE Golden Ages, gain +1 Science Science and +2 Faith Faith for ever… |
| Avicenna | 中世纪 | Gain TechBoosted Eureka for random Medieval Era technology. Religious units gain +3 Stre… |
| Shen Kuo | 中世纪 | This Campus district's Science Science adjacency bonus provides Production Production as… |
| Christopher Clavius | 文艺复兴 | Grants Science Science equal to half of your current Faith Faith output. Allows your bui… |
| Erasmus | 文艺复兴 | While not at War with any civilization, gain +1 FAVOR Diplomatic Favor per turn for each… |
| Louis Pasteur | 工业 | +20% Growth in all cities. Triggers the TechBoosted Eureka for Sanitation. Instantly com… |
| Michael Faraday | 工业 | Chosen City gains +2 Power Power per turn. Triggers TechBoosted Eureka for random Indust… |
| Andrei Sakharov | 信息 | +1 Diplomatic Victory point. Triggers TechBoosted Eureka for random Atomic or Informatio… |

**大工程师（12位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Apollodorus of Damascus | 中世纪 | Each District District in this City yields +1 Production Production and +1 Culture Cultu… |
| Muhammad V | 中世纪 | Grants 3 slots for GreatWork_Landscape Great works of Art to Capital Palace. GreatWork_R… |
| Phidias | 中世纪 | — |
| Vitruvius | 中世纪 | Triggers an TechBoosted Eureka for Engineering and Military Engineering, instantly resea… |
| Jan Adriaanszoon Leeghwater | 文艺复兴 | Chosen city becomes immune to environmental damage. Allows your builders to construct Po… |
| Philibert de l'Orme | 文艺复兴 | Chosen Industrial Zone Production Production adjacency bonus provides equal amount of Cu… |
| Urban | 文艺复兴 | Instantly creates two Bombards with a promotion each. Can be deployed anywhere. |
| Vauban | 文艺复兴 | Instantly creates a Military Engineer. Forts provide +1 Production Production adjacency … |
| Alfred Krupp | 工业 | +25% Production Production towards Siege units. |
| Francesco Bartolomeo Rastrelli | 工业 | — |
| Isambard Kingdom Brunel | 工业 | Chosen city recieves +1% Production Production per unique DISTRICT District type built. |
| Alberto Santos-Dumont | 现代 | Aerodromes receive +2 Production Production and +2 Culture Culture from every adjacent D… |

**大商人（12位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Croesus | 古典 | Doubles current Gold Treasury. |
| Bon da Malamocco | 中世纪 | Activated in foreign Harbor, grants a free GreatWork_Relic Relic and increases TradeRout… |
| Ibn Battuta | 中世纪 | Receive +1 Faith Faith for every 4 tiles a TradeRoute Trade Route travels. |
| Afanasy Nikitin | 文艺复兴 | Grants 1 free copy of the Luxury resource on this tile to your Capital Capital city. Two… |
| Jacob Kettler | 文艺复兴 | Chosen Harbor's adjacency bonuses gain an additional Production Production bonus. Two Ch… |
| Miura Anjin | 文艺复兴 | Grants a free Diplomatic Policy slot in any Government. |
| Alexander Hamilton | 工业 | One extra Economic policy slot in any Government. |
| Cecil Rhodes | 工业 | Instantly creates a Redcoat unit. All your Cities on your non-home Capital Continent wit… |
| Jean Neuhaus II | 工业 | Unlocks TEXTICON_CHOCOLATERIE Chocolaterie - an expensive unique building that grants Cu… |
| Shibusawa Eiichi | 工业 | Each type of Power Power-providing Resource in this City grants +1 Amenities Amenity to … |
| John Pierpont Morgan | 现代 | +1 FAVOR Diplomatic Favor per turn for each Bank. |
| Peter Carl Faberge | 现代 | Creates two copies of RESOURCE_EGG Faberge Eggs, which provide +5 Amenities Amenities ea… |

**大作家（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Augustine of Hippo | 古典 | — |
| Hugo Grotius | 文艺复兴 | Grants +1 Diplomatic Victory point. |
| Friedrich Nietzsche | 工业 | — |
| Jean-Jacques Rousseau | 工业 | Grants +1 Diplomatic Victory point. |
| Voltaire | 工业 | Grants +1 Diplomatic Victory point. |
| H. P. Lovecraft | 现代 | — |
| Martin Heidegger | 现代 | — |
| Robert E. Howard | 现代 | — |
| 罗伯特·舒曼（内部代号DESCARTES） | 原子能 | — |
| 西塞罗 | 原子能 | — |

**大艺术家（2位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| André Le Nôtre | 文艺复兴 | — |
| Lancelot Brown | 工业 | — |

**大探险家（JNR联动）（2位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Ahmad ibn Majid | 文艺复兴 | All Naval units gain +2 Movement Movement. |
| Vitus Bering | 文艺复兴 | Tundra tiles provide +1 GOLD Gold and Snow tiles provide +3 Culture Culture adjacency bo… |


### 3.4 Great Sovereigns大统治者（32条记录）

**大统治者（新类别）（32位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Asoka | 古典 | Cities recieve +1 FAITH Faith and +1 FOOD Food for each Specialty DISTRICT District. |
| Marcus Aurelius | 古典 | Grants CivicBoosted Boost to all Medieval Era Civics. |
| Ptolemy | 古典 | Grants 100 Production Production towards Wonder construction. +1 Culture Culture per Env… |
| Solomon | 古典 | Instantly builds a Temple in this city. Temples provide +2 Production Production. |
| Al-Hakam II | 中世纪 | Cities with a worship building can construct an additional Cathedral, Mosque or Synagoge… |
| Alfred the Great | 中世纪 | — |
| Charlemagne | 中世纪 | One free Military Policy slot in any Government. |
| Enrico Dandolo | 中世纪 | Grants 2 GreatWork_Relic Relics and Relic slots to Capital Palace. TradeRoute Trader Uni… |
| Frederick II | 中世纪 | One free Economic Policy slot in any Government. |
| Harun al-Rashid | 中世纪 | TradeRoute Trade Routes provide +1 SCIENCE Science for every 6 tiles they travel if Civi… |
| Parameswara | 中世纪 | Chosen city gains additional Ranged Attack per turn and yields +5% Gold Gold and FAITH F… |
| Ramkhamhaeng | 中世纪 | All your cities gain +1 Citizen Population for each different type of City-state you are… |
| Vytautas | 中世纪 | Gives chosen city +8 Loyalty per turn and creates a Knight unit with free promotion. Two… |
| Akbar | 文艺复兴 | One free Wild Card Policy slot in any Government. |
| Askia | 文艺复兴 | Conquered cities with a Monument grant a copy of RESOURCE_COWRIE Cowrie - unique Luxury … |
| Isabella I | 文艺复兴 | Grants a free JNR_GreatExplorer Great Explorer. Trader units gain +2 Sight and Naval uni… |
| Ismail I | 文艺复兴 | Capturing a City with Cavalry unit during GLORY_DARK_AGE Dark Age converts it to your ma… |
| Julius II | 文艺复兴 | Grants 455 Production Production towards Wonder construction. |
| Lorenzo the Magnificent | 文艺复兴 | All Renaissance era Wonders in this city gain two slots for GreatWork_Landscape Great Wo… |
| Louis XIV | 文艺复兴 | Grants 3 Slots for GreatWork_Landscape Great Works of Art to all Government Plaza buildi… |
| Maria Theresa | 文艺复兴 | Every type of unique improvement provided by City-States grants +20% GreatArtist Great A… |
| Skanderbeg | 文艺复兴 | Instantly kills all enemy units within 2 tiles. Your land combat units within 2 tiles re… |
| Ulug Beg | 文艺复兴 | Recieve +200 Science Science every time you place a new Campus district. |
| Mehmet Ali | 工业 | 100% Gold Gold discount on all unit upgrades. Grants one randomly-chosen free technology. |
| Meiji | 工业 | Replacing a Farm with an Industrial zone or Neighborhood grants a burst of GOLD Gold. In… |
| Otto von Bismark | 工业 | Become Suzerain of chosen City-state, removing all other players Envoy Envoys. +1 Favor … |
| Prithvi Narayan Shah | 工业 | +3 Strength Combat Strength to all melee and ranged land units. Additional +3 Strength C… |
| Ataturk | 现代 | Grants 400 PRODUCTION Production towards any Construction or Unit training. Three Charge… |
| Haile Selassie | 现代 | Grants +2 Diplomatic Victory points. |
| Lee Kuan Yew | 原子能 | GreatMerchant Great Merchants gain +1 Charges Charge. |
| Zayed bin Sultan Al Nahyan | 原子能 | Your cities receive +20% GOLD Gold for each different Power Power-providing Strategic Re… |
| Rainier III | 信息 | Grants 200 Tourism Tourism per excess copy of the Luxury resources that you currently po… |


### 3.5 平等伟人科学家（25条记录）

**大科学家（8位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Theophrastus | 古典 | This Campus district's Science Science adjacency bonus provides Food Food as well. |
| William of Ockham | 中世纪 | — |
| Fritz Haber | 现代 | Farm tiles gain +1 Food Food per turn. |
| Marie Curie | 现代 | Instantly builds the Radium Institute, a unique building that provides +3 Science Scienc… |
| Satyendra Nath Bose | 现代 | — |
| Wilhelm Röntgen | 现代 | Gain {Amount : number #} Science Science. |
| Stephen Hawking | 原子能 | — |
| Tim Berners-Lee | 信息 | Gain {Amount : number #} Science Science. |

**（修改原版伟人）（17位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 伽利略 | — | — |
| 卡尔·萨根 | — | — |
| 图灵 | — | — |
| 埃米莉·杜夏特莱 | — | Gain {Amount : number #} Science Science. |
| 希帕提娅 | — | — |
| 扎哈拉维 | — | — |
| 斯蒂芬妮·克沃莱克 | — | Invents Kevlar, providing +10 Strength defense strength to all units. |
| 欧几里得 | — | Gain {Amount : number #} Science Science. |
| 海什木（欧玛尔·海亚姆） | — | Gain {Amount : number #} Science Science. + This Campus district's Science Science adjac… |
| 爱因斯坦 | — | — |
| 牛顿 | — | — |
| 薛定谔 | — | — |
| 诺贝尔 | — | — |
| 达尔文 | — | — |
| 门捷列夫 | — | Instantly builds the Mendeleev Institute for Metrology, a unique building that provides … |
| 阿卜杜斯·萨拉姆 | — | Instantly builds the Abdus Salam Centre for Theoretical Physics, a unique building that … |
| 阿耶波多 | — | Instantly builds the University of Nalanda, a unique building that provides +2 Science S… |


### 3.6 平等伟人工程师（14条记录）

**大工程师（10位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Banū Mūsā | 中世纪 | — |
| Francesco di Giorgio | 文艺复兴 | Instantly builds Ancient, Medieval, and Renaissance Walls in this city. |
| Johannes Gutenberg | 文艺复兴 | Instantly builds Gutenberg's Workshop, a unique wonder with +3 Faith Fatih and +3 Produc… |
| Frederick Olmsted | 工业 | Instantly builds Central Park, a unique wonder with +2 Amenities amenities, in a city ce… |
| Isambard Brunel | 工业 | Instantly builds the Great Western Railway in a city center, a wonder that provides +2 C… |
| Alexander Fleming | 现代 | Instantly adds +3 Citizen Population to a single city. |
| Hedy Lamarr | 现代 | Invents the Secret Communications System, providing +5 Strength combat strength to all M… |
| Fazlur Rahman Khan | 原子能 | — |
| Gurmukh Sarkaria | 原子能 | Instantly builds the Itaipu Dam in an Industrial Zone, a wonder that provides +20 Produc… |
| Mars Exploration Rover Team | 信息 | +{Amount}% Production Production towards Space Race projects. |

**（修改原版伟人）（4位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 毕昇 | — | This Industrial Zone's Production Production adjacency bonus provides Culture Culture as… |
| 简·德鲁 | — | +{Amount} Amenities {Amount : plural 1?Amenity; other?Amenities;} for this city. |
| 约翰·罗布林 | — | Instantly builds the Brooklyn Bridge in a city center, a wonder that provides +4 Culture… |
| 莱昂纳多·达·芬奇 | — | — |


### 3.7 平等伟人商人（16条记录）

**大商人（11位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| Hippalus | 古典 | Grants {Amount} RESOURCE_AOM_PEPPER Pepper, a unique Luxury resource which provides +4 A… |
| Kanishka | 古典 | — |
| Dick Whittington | 中世纪 | Instantly builds Whittington's College, a unique building with +3 Housing housing, in a … |
| Ichtacka Pochteca | 中世纪 | Grants {Amount} RESOURCE_AOM_TURQUOISE Aztec Turquoise, a unique Luxury resource which p… |
| Joseph of Spain | 中世纪 | Grants {Amount} RESOURCE_AOM_JOSEPH_OF_SPAIN_SAFFRON Saffron, a unique Luxury resource w… |
| James Lancaster | 文艺复兴 | Instantly builds the East India Company, a unique building that gives +1 Gold gold for e… |
| David Ogilvy | 现代 | +1 Wildcard policy slot in any government. |
| David Sarnoff | 现代 | Instantly builds the National Broadcasting Company (NBC), a Wonder that provides +5 Gold… |
| Lizzie Magie | 现代 | Grants {Amount} RESOURCE_AOM_BOARD_GAMES Board Games, a unique Luxury resource which pro… |
| Raymond Rubicam | 原子能 | This Commercial Hub district's Gold Gold adjacency bonus provides Culture Culture as well. |
| Jeff Bezos | 信息 | Grants {Amount} RESOURCE_AOM_E_BOOKS E-Books, a Luxury resource which provides +6 Amenit… |

**（修改原版伟人）（5位）**

| 伟人 | 时代 | 效果 |
|---|---|---|
| 乔瓦尼·德·美第奇 | — | Instantly builds the Medici Bank, a unique building with +2 Gold gold, and +1 GreatMerch… |
| 拉贾·托达尔·马尔 | — | Farm tiles in this city gain +1 Gold per turn. |
| 约翰·雅各布·阿斯特 | — | — |
| 莎拉·布里德洛夫 | — | Grants {Amount} RESOURCE_AOM_SARAH_BREEDLOVE_HAIRCARE_PRODUCTS Hair Care Products, a uni… |
| 雅各布·富格尔 | — | Instantly builds the Fuggerei in this district, a unique building with +3 Housing housin… |


---

## 四、重叠、冲突与空白位分析

### 4.1 跨 mod 重复人物（同一历史人物被多个mod使用）

| 人物 | 出现的mod | 冲突说明 |
|---|---|---|
| 扬·杰什卡 Jan Zizka | Nyguita（大将军）+ Sumus Magnus（大将军） | 同人类重复，整合时二选一 |
| 詹姆斯·库克 James Cook | Nyguita（海军统帅）+ Sumus Magnus（海军统帅） | 同人类重复 |
| 达·芬奇 | AOM工程师（改为**大艺术家**）+ 原版（工程师）+ Sumus 无 | AOM直接改类别，整合时需决策 |
| 玛丽·居里 | AOM科学家（新版，建镭研究所）+ 原版无居里（原版无此人，GS为新增？否——原版无居里） | AOM新增 |
| 法拉第 Faraday | Team PVP（工程师，供电15回合）+ Sumus Magnus（科学家，可选） | **跨类别重复**，需决策类别 |
| 蔡伦/沈括等中国科学家 | Sumus Magnus 新增 | 与 Nyguita 的孙思邈等中国伟人主题重叠但人物不同 |
| 伊莎贝拉/玛丽亚·特蕾莎等君主 | Great Sovereigns | 与文明领袖不同（作为伟人而非领袖），无直接冲突 |
| 爱因斯坦/牛顿/伽利略等 | AOM 科学家（全部重做） | 与原版同名替换 |

### 4.2 AOM 三部曲删除/替换的原版伟人（移植时必须成对处理）

| 原版伟人 | AOM处理 | 替代方案 |
|---|---|---|
| 伽利略、牛顿、达尔文、诺贝尔、图灵、爱因斯坦、薛定谔、萨根 | 删效果→产"科学巨作" | 巨作+4~+8科技/文化 |
| 阿耶波多、门捷列夫、居里（新增）、萨拉姆 | 改为建专属建筑 | 世界唯一建筑（那兰陀大学等） |
| 欧几里得、海什木、杜夏特莱、伦琴（新增）、伯纳斯-李（新增） | 改为一次性科技值 | 120~1850科技 |
| 希帕提娅、扎哈拉维、奥卡姆（新增）、玻色（新增）、霍金 | 产科学巨作/被动 | — |
| Janaki Ammal、James Young | **直接删除** | 被新版本替换 |
| 达·芬奇（工程师） | **改为大艺术家** | 产《蒙娜丽莎》等3件艺术巨作 |
| 阿达·洛芙莱斯、戈达德、冯·布劳恩（工程师） | **直接删除** | 改为科学家版/被替换 |
| 克拉苏、伊琳娜、戈达德、本茨、巴尔迪（商人） | **直接删除** | 被新版本替换 |
| 美第奇、富格尔、阿斯特、布里德洛夫、托达尔·马尔等（商人） | 效果重做 | 专属建筑/新机制 |

### 4.3 时代×类别空白位（原版+全部mod后仍然稀疏的位置）

| 类别 | 原版最稀疏时代 | mod补充情况 | 仍空白 |
|---|---|---|---|
| 大作家 | 原子能2、信息2 | TPMG+23位（全覆盖到信息） | 未来时代 |
| 大艺术家 | 信息4 | Nyguita+11（含未来？否，到信息） | 未来时代 |
| 大音乐家 | 信息2 | Nyguita+11（含2位未来时代！） | — |
| 大工程师 | 中世纪4 | 各mod补充充分 | — |
| 大商人 | 古典3 | TPMG/Nyguita/Sumus均补古典 | — |
| 大科学家 | 信息3 | 各mod补充充分 | — |
| 大将军 | 信息2 | TPMG补到现代，Nyguita补到现代 | 原子能/信息仅原版 |
| 大海军统帅 | 信息1 | Nyguita+11（到原子能） | 信息时代稀缺 |
| 大先知 | — | **无人补充** | **完全空白** |
| 大统治者 | — | Sovereigns新增32位 | 新类别 |

---

## 五、移植蓝图：单个伟人移植的最小文件要素

以"从某个mod抽1位伟人放进自己的新mod"为单位，每个伟人需要搬运的部件：

| 部件 | Team PVP 型（SQL） | Nyguita/Sumus 型（XML） | AOM 替换型 |
|---|---|---|---|
| 伟人定义 | `INSERT INTO GreatPersonIndividuals` | `<GreatPersonIndividuals><Row>` | 同名 Delete+Insert |
| 效果修饰器 | `Modifiers`+`ModifierArguments`+`GreatPersonIndividualActionModifiers` | 同名XML表 | 同左 |
| 出生修饰器（将军/统帅光环） | `GreatPersonIndividualBirthModifiers` | 同左 | 同左 |
| 巨作定义（作家/艺术家/音乐家） | `GreatWorks` 表 + 著作文本 | `GreatWorks.xml` | 科学/工程巨作+伪产出类型 |
| 本地化文本 | `LocalizedText`（中英文） | `<LocalizedText>`（仅英文，需自译） | 英/法文，需自译 |
| 图标 | `TPMG_ICONS.sql` 段 | `Great_People_Icons.xml` + DDS | Icons.xml + artdef + BLP |
| 特殊机制 | Lua（如詹天佑铁路寻路、UI请求） | 无/少量 | UI替换Lua（**勿移植**） |
| 依赖建筑/资源 | 部分（医疗兵等） | 部分（Sumus专属建筑/资源） | 必须连带（专属建筑/奢侈品） |

**移植难度评级：**

- ★ 简单：纯巨作产出型（作家/艺术家/音乐家，如 Nyguita 全部、TPMG 作家音乐家）——只涉及3张表+文本
- ★★ 中等：一次性效果型（大多数科学家/商人/工程师）——需移植 Modifiers 链
- ★★★ 复杂：带光环/被动/Lua 逻辑（TPMG 将军、詹天佑、AOM 建筑型、Sovereigns 全体）——需连带基础设施

---

## 六、下一步

本文档是移植底稿。接下来用 grilling 拷问收敛以下决策：目标规则集（GS是否必需）、新mod定位（替换型还是新增型）、各类伟人数量预算、重复人物取舍、每个伟人的去留与效果定稿。
