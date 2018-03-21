# 麻将胡牌算法
带鬼牌（癞子）的胡牌算法，采用查表方式，能够知道胡哪张牌

# 牌型分类
- 普通牌：万筒条，每门有序数从一至九的牌各四张
- 风牌：東、南、西、北
- 箭牌：中、發、白


# 术语
- 连子：一万二万三万
- 刻子：一筒一筒一筒
- 将：一条一条


# 胡牌规则
- N×连子 + M×刻子 + 将
- N>=0,M>=0

# 牌型编码
- 按照花色分成几组数字
- 例如1万2万5万5万：110020000，左数第M位是N，说明M万有N张
- 这样万筒条风箭，就有5个数字key

# 表生成
- 分为普通、风、箭三张表
- 对于每个key，生成这个key可以胡的信息列表
- 例如1万2万5万5万：110020000，生成的胡牌信息有
- 1万2万5万5万：鬼0 有将 胡3万（0个鬼的时候，这个牌胡3万，此时有将）
- 1万2万5万5万：鬼1 无将 胡3万胡5万（1个鬼的时候，这个牌胡3万5万，此时无将）
- 1万2万5万5万：鬼1 有将 胡了（1个鬼的时候，这个牌已经胡了（鬼变成3万），此时有将）
- ...

# 胡牌算法
- 对玩家手上的牌进行编码，变成5个key和鬼牌总数N
- 对每个key查询表，得到5组胡牌信息列表
- 简单递归下，看看5组胡牌信息列表里，是否满足鬼的总数和只有一个将的约束，同时每个花色都是胡了
- 耗时也就是：查表耗时*5 + 递归5层分配鬼和将的耗时

# 查胡算法
- 与胡牌算法类似，根据key查出胡牌信息列表
- 简单递归下，找出满足鬼的总数和只有一个将的约束时，所有不能胡的胡牌信息里可胡牌的集合，就是这手牌能胡什么牌
- 优化，比如已经知道能胡1万2万3万，那么就不再去递归胡2万（子集）的可能

# 其他
- 目前生成了sqlite和txt两种方式，可以修改规则重新生成，比如有的麻将东西南也算连子

