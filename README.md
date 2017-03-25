長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Loading required package: xml2

``` r
ptt <- "https://www.ptt.cc/bbs/Tech_Job/index.html"

ptt_data = c()
for(i in 1:10){
  
  ptt_title <- read_html(ptt) %>% html_nodes(".title") %>% html_text
  ptt_pushnum <- read_html(ptt) %>% html_nodes(".nrec") %>% html_text
  ptt_author <- read_html(ptt) %>% html_nodes(".author") %>% html_text
  pttcon <- data.frame(title = ptt_title,num = ptt_pushnum,author = ptt_author)
  ptt_data <- rbind(ptt_data,pttcon)
  ptt_link <- read_html(ptt) %>% html_node(".btn-group-paging a:nth_child(2)") %>% html_attr("href")
  ptt <- paste0('https://www.ptt.cc',ptt_link)

}
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(
    ptt_data[c("title","num","author")]) 
```

| title                                                       | num | author       |
|:------------------------------------------------------------|:----|:-------------|
| \[聘書\] Offer請益 達創/新日興                              | 7   | lovetire     |
| \[請益\] Offer請益 英業達/鴻海                              | 4   | kusahara     |
| 律師為您解惑－線上勞動法免費諮詢即日為勞工 … 爆             | pz  | s            |
| \[公告\] Tech\_Job板板規 2014.03.01                         | 7   | mmkntust     |
| \[公告\] 置底 檢舉/推薦 文章                                | 爆  | mmkntust     |
| \[免費\]工作人生顧問                                        | 爆  | zodiac       |
| \[心得\] 面試 大立光電/艾克爾/采鈺/百佳泰/美光              | 10  | goodboy8899  |
| \[請益\] 電機女生找工作                                     | 68  | alice2520200 |
| \[心得\] 我在拓凱(台中工業區)的日子                         | 48  | dash0804     |
| Re: \[心得\] 群聯不舒服的面試經驗                           | 8   | magic704226  |
| \[請益\] 新人一個月提離職                                   | 26  | catdogter    |
| 台積0972006688                                              | 1   | stan1111     |
| (本文已被刪除) \[wort\]                                     |     | -            |
| \[請益\] 內湖緯創ＥＢＧ情況                                 | 8   | wort         |
| (本文已被刪除) \[sopi\]                                     |     | -            |
| \[請益\] 在台灣工作未來方向                                 | 14  | omega0210    |
| \[請益\] 陶氏化學CDP面試詢問                                |     | chengyuche   |
| \[請益\] 做Power ICdesign的前景？                           | 23  | golover      |
| (本文已被刪除) \[imch543\]                                  | 1   | -            |
| \[討論\] 關於機台零件是不是都撐到最後？                     | 13  | s4001        |
| \[討論\] 關於伺服器代工                                     | 10  | orz3qonz     |
| \[請益\] 請問有人了解三浦鍋爐嗎                             |     | skatopia     |
| \[新聞\]【台GG別走動畫】台積傳將赴美砸5千億建3              | 29  | DickMartin   |
| \[新聞\] 靠文青打敗台積電　新鮮人最嚮往企業出爐             | 36  | popoallan    |
| \[聘書\]台灣公司以及大陸公司歐菲光                          | 4   | sht255       |
| ［疑惑］台GG要在竹南設廠的傳聞有下文嗎？                    | 18  | q99518g      |
| (本文已被刪除) \[KFCNTU\]                                   | 6   | -            |
| Re: \[新聞\] 科技RD「每天7點下班」超貼心　台女              | 2   | join183club  |
| \[心得\] 群聯不舒服的面試經驗                               | 42  | wears        |
| (本文已被刪除) \[llloser\]                                  | 29  | -            |
| (本文已被刪除) \[tako30215\]                                |     | -            |
| \[討論\] 面試有補助交通費的有那些公司?                      | 43  | magic704226  |
| \[新聞\] 聯發科Q1營業淨利恐季減70%                          | 37  | unrest       |
| \[請益\] offer選擇 力晶/景碩                                | 3   | blacksky124  |
| Re: \[公司\] 大船集團-達航科技                              |     | pinkowa      |
| \[請益\] 系統廠HW 能轉甚麼職缺?                             | 9   | sustaned     |
| \[聘書\] offer請益 華碩/彩富/矽創                           | 6   | wuhalala     |
| \[請益\] 正文是屬於ic design的公司嗎？                      | 1   | ghost1006    |
| \[請益\] 請問日本還有能打的半導體廠嗎                       | 9   | lin214       |
| \[請益\] 覆晶封裝製程轉職問題                               | 14  | KFCNTU       |
| \[新聞\] 華爾街日報：印度即將開始生產iPhone                 | 3   | Lanaroh      |
| \[徵才\] ucfunnel-媒體開發/PM/Node.js/Frontend              | 1   | livingroom   |
| \[請益\] 第一份工作薪水重要還是練功重要?                    | 86  | s6307        |
| Re: \[請益\] 覆晶封裝製程轉職問題                           | 6   | gnh1021      |
| \[請益\] 研發替代役                                         | 6   | leo710215    |
| \[請益\]offer選擇                                           | 9   | david597     |
| Re: \[請益\] 環球水泥與耐落螺絲                             | 4   | giggled      |
| \[討論\] 要求先提供照片 涉及違反就服法???                   |     | seedhyper    |
| (本文已被刪除) \[xvideos\]                                  | 75  | -            |
| Re: \[請益\]信鼎技術 面試前準備?                            |     | AlioAlio     |
| (本文已被刪除) \[crazyjen\]                                 | 14  | -            |
| \[請益\] 克達科技(安捷倫電子量測儀器代理)                   | 1   | dmgucci      |
| \[新聞\] 蔡力行轉戰聯發科 台積電發表看法了                  | 28  | kof70380     |
| \[請益\]請問威剛的工作狀況                                  | 4   | rock913343   |
| \[討論\] 美商Ubiquiti Networks優比快                        | 10  | aaron2034b   |
| Re: \[討論\] 鈞立科技(最新力作再現)                         | 1   | lkklkksppspp |
| \[請益\] C++有沒有類似SCJP的題庫                            | 4   | Nippey       |
| \[請益\] 哪條路，若想轉職比較方便？                         | 10  | a40232145    |
| \[請益\] 戀人最近在忙什麼？                                 | 13  | leatica      |
| \[請益\] 想詢問面試狀況                                     | 1   | howdai123    |
| \[新聞\] 鐵血CEO蔡力行扮「殺手」？聯發科員工剉              | 45  | tw689        |
| (已被mmkntust刪除) <popularman> 版規六                      | 1   | -            |
| \[請益\] 業務工程師 北區推薦                                | 6   | praive       |
| \[新聞\] 首年享13天特休！德州儀器徵100人　研究所畢起薪5-6萬 | 10  | wer11        |
| \[新聞\] 國防55級分 畢業「免當軍人」上班月領51K             | 3   | s6307        |
| \[新聞\] 科技RD「每天7點下班」超貼心　台女竟怒              | X1  | AK47shoot    |
| \[討論\] 中部某封測廠的面談經驗                             | 8   | stennis      |
| \[新聞\] 【震驚科技業】蔡力行轉戰聯發科　是否               | 36  | wahaha23     |
| (本文已被刪除) <A2GMAT>                                     |     | -            |
| \[請益\] 奇美材料到底好不好= =                              | 13  | esp0122      |
| \[請益\] 力晶元件助理工程師                                 | 12  | PTT1774      |
| \[請益\] 大公司的APR 跟小公司的數位IC                       | 17  | qqr29        |
| \[心得\] AMAT/Ultratech/mattson/Rudolph/ASM                 | 23  | roy10531     |
| Fw: \[公司\] 大船集團-達航科技                              | 3   | Miwaitte     |
| (本文已被刪除) \[Ferrara\]                                  | 8   | -            |
| (本文已被刪除) \[mimicat0228\]                              | 13  | -            |
| \[請益\] 仁寶 智慧型裝置 android                            | 12  | jenny920218  |
| \[請益\] 台汽電公司待遇及福利如何                           | 2   | s357678      |
| Re: \[討論\] 台塑or中油                                     | 20  | turn329      |
| \[新聞\] 蔡力行轉戰聯發科 網友：員工苦日子到                | 22  | cychine      |
| \[請益\] 聯電/美光/友達 選擇                                | 37  | suryany      |
| \[請益\] 環球水泥與耐落螺絲                                 | 7   | e3472419     |
| (本文已被刪除) \[wears\]                                    | 25  | -            |
| Re: \[請益\] 仁寶 智慧型裝置 android                        | 3   | ABCcomputer  |
| \[請益\] 南科 新世紀光電公司好嗎??                          | 5   | zgmfx0326    |
| (本文已被刪除) \[giggled\]                                  |     | -            |
| \[請益\] 緯創server部門好嗎?                                | 8   | fantacy0225  |
| \[請益\] 尋求找工作方向建議                                 | 2   | YWEC         |
| \[新聞\] 聯發科訂單沒跟上                                   | 3   | unrest       |
| Re: \[討論\] 台積電有可能成為百年企業嗎 ?                   | 6   | bluejade1235 |
| \[新聞\] 聯詠員工分紅打6折 群聯大方送5.5億增1成             | 6   | gn01216674   |
| \[討論\]報到的第二個禮拜想離職.......                       | 8   | judy79702    |
| Re: \[討論\]報到的第二個禮拜想離職.......                   | 53  | join183club  |
| \[面試\] 在linkedin上找工作 就不會被原公司發現?             | 5   | sustaned     |
| \[請益\] 錄取未報到..                                       |     | qqdnsr       |
| \[請益\] 首岳資訊網路股份有限公司                           |     | edison81630  |
| (本文已被刪除) \[csro7788\]                                 | 22  | -            |
| Re: \[討論\] 台積電有可能成為百年企業嗎 ?                   | 8   | lovebridget  |
| 長春彰濱廠                                                  | 6   | adidasshow   |
| \[情報\] 英特爾購併Mobileye是追夢還是夢靨？                 | 6   | zxcvxx       |
| Re: \[討論\]報到的第二個禮拜想離職.......                   | 5   | hidog        |
| Re: \[討論\]報到的第二個禮拜想離職.......                   |     | pinkowa      |
| \[請益\] 鴻勝化學&宏騰光電...                               | 3   | qqming0721   |
| \[討論\] 台塑or中油                                         | 77  | Mason61931   |
| \[新聞\] 蔡力行轉戰聯發科 網友：員工苦日子到                | 38  | jeromeshih   |
| \[請益\] 英業達Server的power team                           | 3   | middux       |
| \[請益\] 友達 美光 力晶 哪家最推薦去呢?                     | 45  | okopp        |
| \[請益\] 面試請益                                           | 3   | lhx63524     |
| 資料探勘及資料分析的基本能力為何                            |     | uasalada     |
| \[請益\] 元隆電子                                           | 2   | zyxcba5      |
| (本文已被刪除) \[parrotQQ\]                                 | 16  | -            |
| \[請益\] FAE面試請益                                        | 30  | lovelyjojo   |
| (已被lovewsc刪除) <Sunday1990>版規一                        | 2   | -            |
| Re: \[新聞\] 聯發科宣布 蔡力行接共同執行長、集團副          | 14  | a875979      |
| (本文已被刪除) \[smho\]                                     |     | -            |
| \[請益\] 晶電 vs 鼎元 (竹南)                                | 8   | kkkmaxtine   |
| \[討論\] 晶睿通訊                                           | 5   | tiyico       |
| \[請益\] gg設備幹到頂天有機會被高薪挖角嗎                   | 4   | onlytiger    |
| \[討論\] 新人離職                                           | 74  | forgood      |
| (本文已被刪除) \[PTTcrazy\]                                 | 1   | -            |
| \[請益\]男生做友達OP 適合待到退休嗎?                        | 18  | Silent       |
| \[討論\] 陣亡率高/免洗的職位                                | 24  | NTUlosers    |
| \[討論\] 科技業公司一虧損就開始拆子公司是常態嗎             | 14  | gotptt       |
| \[徵才\] Taylormade Golf company (高雄辦公室)               |     | loddy        |
| \[討論\] 台積電有可能成為百年企業嗎 ?                       | 9   | goodpoint    |
| \[請益\]華新科福利                                          | 4   | ichior       |
| \[情報\] (代po)科技人面試求職講座                           | 6   | yunnnn       |
| Re: \[請益\]信鼎技術 面試前準備?                            | 7   | AlioAlio     |
| Re: \[新聞\] 斥資600億 「綠能科學城」落腳台南沙崙           | 13  | juangpeiyi   |
| \[請益\] offer 選擇                                         | 6   | eclipse911   |
| \[討論\] 系統廠的生命力是否比較強？                         | 8   | join183club  |
| \[請益\] 有人聽過Sogeti這間公司嗎                           | 1   | takeon       |
| \[請益\] offer 選擇                                         | 1   | chrishyper   |
| \[新聞\] 「中國製造2025」美憂威脅國安                       | 12  | AAAB         |
| \[請益\] 菱X科技                                            | 10  | maxgxking    |
| \[新聞\] 環評空污缺電 黃士修：台積電快走吧!                 | 31  | wahaha23     |
| \[請益\] htc派遣問題                                        |     | seal44       |
| (本文已被刪除) \[mrasta\]                                   |     | -            |
| \[新聞\] 傳蔡力行 跳槽聯發科(已公告)                        | 53  | http405      |
| Re: \[新聞\] 傳蔡力行 跳槽聯發科                            | 10  | jeromeshih   |
| \[新聞\] 聯發科宣布 蔡力行接共同執行長、集團副              | 72  | RTA          |
| (本文已被刪除) \[VULPIG\]                                   |     | -            |
| Re: \[請益\] Nvidia的Android Framework/SW Engineer          | 5   | nixt         |
| \[請益\] 敏實集團 minth group                               | 1   | urocissa     |
| \[聘書\] 研替offer詢問(QNAP/緯創)                           | 5   | lebron0426   |
| Re: \[新聞\] 傳蔡力行 跳槽聯發科(已公告)                    | 15  | TSMCer       |
| \[請益\] 竹科聯電製程                                       | 9   | berac16      |
| \[新聞\] 讀軍校免當軍人 中科院上班54K                       | 18  | tw689        |
| \[請益\] 日月光-歐美區(美國)客戶關係管理                    | 11  | lim10337     |
| \[請益\] 南科住華科技                                       | 12  | kurtgod      |
| \[請益\] Nvidia的Android Framework/SW Engineer              | 16  | magic704226  |
| \[請益\] 亞德客or鑫陽鋼鐵                                   | 6   | eraser90310  |
| \[請益\] 云辰科技                                           |     | Intelgence   |
| \[請益\] NXP Service Engineer                               | 7   | angelpeace   |
| \[情報\] 千竣科技違反勞基法，官司結果                       | 49  | GameHeven    |
| \[新聞\] 台積電試產 7 奈米良率超過七成                      | 42  | unrest       |
| (本文已被刪除) \[scntu\]                                    |     | -            |
| \[請益\] 台積電的設備自己研發?                              | 55  | sustaned     |
| \[請益\] offer選擇                                          | 7   | queenghost   |
| \[討論\] 公司要資遣人，需要通報勞工局嗎？                   | 12  | JE2K         |
| \[新聞\] 新日光虧損破紀錄 去年財報淨損63.1億                | 16  | moonth66     |
| \[新聞\] 竹科IC產業衰退？ 科管局：研發力道仍強              | 8   | breath35     |
| (本文已被刪除) \[yichun1299\]                               |     | -            |
| \[請益\] 走品質的有可能年薪破百嗎?                          | 21  | DUFA         |
| \[討論\] 板上有人遇過這種情況嗎                             | 4   | forgetwhat   |
| \[請益\] 在台灣只剩下一年 該換工作嗎?                       | 9   | kissyourbi   |
| (本文已被刪除) \[crt0921\]                                  | 5   | -            |
| (已被m刪除) <qazxc1156892> \#1GyZ6pe7                       |     | -            |
| Re: \[新聞\] 績效獎金打6折？ 聯詠：不予回應                 | 3   | jeromeshih   |
| Re: \[請益\] 水果公司的工廠，工程師好跳嗎？                 |     | typewindow   |
| Re: Fw: \[新聞\] 新世代最崇拜企業家　郭董取代賈柏斯         |     | jeromeshih   |
| \[心情\] 連來台灣的外國朋友都會講"台積電"華文               | 8   | terimakasih  |
| \[請益\] 獵人頭 網站 or APP                                 | 16  | sustaned     |
| \[新聞\] 台積電赴美設廠？ 科技部轉述：並無此計              | 19  | TrueSpace    |
| \[請益\] 螃蟹OFFER請益(代PO)                                | 6   | birdhackor   |
| \[請益\] 以下加班申請定合理嗎?                              | 9   | zaxck        |
| (本文已被刪除) \[Qoo2\]                                     | 18  | -            |
| Re: \[請益\] 獵人頭 網站 or APP                             | 8   | appledavid   |
| \[請益\] 半年的技術員經歷                                   | 16  | ak080775     |
| \[請益\] 宏騰光電一些問題...                                | 3   | qqming0721   |
| Fw: \[徵才\] 興豪傳媒科技 誠徵Javascript前端工程師          | 1   | cliffk321    |
| \[請益\] 福爾摩莎紙業股份有限公司高雄業務                   |     | edison81630  |
| \[聘書\] 研替offer請益(皮卡)                                | 5   | paulu90      |
| \[新聞\] 吞iPhone緯創資本支出破百億　3年新高                | 11  | qazxc1156892 |
| (本文已被刪除) \[as123as41\]                                |     | -            |
| \[新聞\] 陳良基：與張忠謀溝通過「所有投資以台灣為優先       | 12  | wer11        |

解釋爬蟲結果
------------

``` r
str(ptt_data)
```

    ## 'data.frame':    186 obs. of  3 variables:
    ##  $ title : Factor w/ 180 levels "\n\t\t\t\n\t\t\t\t[公告] 置底 檢舉/推薦 文章\n\t\t\t\n\t\t\t",..: 4 5 6 2 1 3 20 11 21 26 ...
    ##  $ num   : Factor w/ 49 levels "4","7","爆","",..: 2 1 3 2 3 3 6 15 14 16 ...
    ##  $ author: Factor w/ 139 levels "kusahara","lovetire",..: 2 1 4 3 3 5 13 7 10 14 ...

``` r
tem <- table(ptt_data$author)
sort(tem,decreasing = T)
```

    ## 
    ##            -     sustaned   jeromeshih  magic704226  join183club 
    ##           27            4            4            3            3 
    ##       unrest     mmkntust      pinkowa        s6307     AlioAlio 
    ##            3            2            2            2            2 
    ##        tw689        wer11     wahaha23  edison81630   qqming0721 
    ##            2            2            2            2            2 
    ##     kusahara     lovetire          pzs       zodiac alice2520200 
    ##            1            1            1            1            1 
    ##    catdogter   chengyuche     dash0804   DickMartin      golover 
    ##            1            1            1            1            1 
    ##  goodboy8899    omega0210     orz3qonz    popoallan      q99518g 
    ##            1            1            1            1            1 
    ##        s4001       sht255     skatopia     stan1111         wort 
    ##            1            1            1            1            1 
    ##  blacksky124     david597    ghost1006      gnh1021       KFCNTU 
    ##            1            1            1            1            1 
    ##      Lanaroh    leo710215       lin214   livingroom        wears 
    ##            1            1            1            1            1 
    ##     wuhalala    a40232145   aaron2034b    AK47shoot      dmgucci 
    ##            1            1            1            1            1 
    ##      giggled    howdai123     kof70380      leatica lkklkksppspp 
    ##            1            1            1            1            1 
    ##       Nippey       praive   rock913343    seedhyper  ABCcomputer 
    ##            1            1            1            1            1 
    ##      cychine     e3472419      esp0122  jenny920218     Miwaitte 
    ##            1            1            1            1            1 
    ##      PTT1774        qqr29     roy10531      s357678      stennis 
    ##            1            1            1            1            1 
    ##      suryany      turn329    zgmfx0326   adidasshow bluejade1235 
    ##            1            1            1            1            1 
    ##  fantacy0225   gn01216674        hidog    judy79702  lovebridget 
    ##            1            1            1            1            1 
    ##   Mason61931       middux       qqdnsr         YWEC       zxcvxx 
    ##            1            1            1            1            1 
    ##      a875979      forgood    goodpoint       gotptt       ichior 
    ##            1            1            1            1            1 
    ##   kkkmaxtine     lhx63524        loddy   lovelyjojo    NTUlosers 
    ##            1            1            1            1            1 
    ##        okopp    onlytiger       Silent       tiyico     uasalada 
    ##            1            1            1            1            1 
    ##      zyxcba5         AAAB   chrishyper   eclipse911      http405 
    ##            1            1            1            1            1 
    ##   juangpeiyi   lebron0426    maxgxking         nixt          RTA 
    ##            1            1            1            1            1 
    ##       seal44       takeon       TSMCer     urocissa       yunnnn 
    ##            1            1            1            1            1 
    ##   angelpeace      berac16     breath35         DUFA  eraser90310 
    ##            1            1            1            1            1 
    ##   forgetwhat    GameHeven   Intelgence         JE2K   kissyourbi 
    ##            1            1            1            1            1 
    ##      kurtgod     lim10337     moonth66   queenghost     ak080775 
    ##            1            1            1            1            1 
    ##   appledavid   birdhackor    cliffk321      paulu90 qazxc1156892 
    ##            1            1            1            1            1 
    ##  terimakasih    TrueSpace   typewindow        zaxck 
    ##            1            1            1            1

186obs. 因此共爬出186篇文章

先使用table了解每個作者po文幾次， 在使用sort排序，排出次序， “-”為刪文，因此文章最多的作者為“sustaned”和“jeromeshih”都是4次。

``` r
#這是R Code Chunk
```

由上面的sort我們可以知道， 一般人在Tech\_Job版上po文大多為1則， 只有少數人為2則以上。

而超過2則po文的作者， 大多主題跟“請益”或是“新聞”有關， 只有少部分的人是有關其他部分的。

另外從上方的186則結果中， 發現只有3篇的推文數來到“爆”， 分別是“律師為您解惑－線上勞動法免費諮詢即日為勞工 …”、“\[公告\] 置底 檢舉/推薦 文章” 和“\[免費\]工作人生顧問”， 而這三篇文也是位於版主設定的置底文， 推測是因為此版已鎖定在科技業上， 大多都是從事科技業的人會看的版， 不像NBA、八卦版等版， 較為一般人也會瀏覽的版， 因此本身來到推文來到“爆”的文章相對來說少很多。
