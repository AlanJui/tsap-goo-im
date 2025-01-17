# Neovim 搜尋與替換指引

## 字典批次替換

漢字詞庫檔（Text File），其內容如下：

```sh
a	仔
aa	噯仔
aa	尪仔
aa	押後
aa	暗安
aa	楬仔
aa	甌仔
aa	甕仔
aa	盒仔
aa	遏泔
aa	鴨仔
aab	尪仔面
aab	翁仔某
aak	頷仔頸
aak	鴨仔囝
aam	尪仔物
aan	頷仔領
aap	盒仔餅
aaph	尪仔標
aat	鴨仔癉
aath	尪仔頭
aathh	嘔紅吐血
aats	尪仔書
aatsh	尪仔冊
ab	壓味
ab	安眠
```

每行結構：（羅馬字拼音）\t（漢字詞彙）\t（註釋）\n

【註】： 上述的「註釋」，經常為「空」，沒有文字在內。

上述結構欲變更為：（漢字詞彙）\t（羅馬字拼音）\t（註釋）\n

使用指令架構如下：

:%s/^(...X...)\\t(...Y...)\\t(...Z...)$/$2\t\$1\$3$/g

```sh
:%s/^\(\a\+\)\t\(\S\+\)\t\(.*\)$/\2\t\1\t\3/g
```

## 參考

### 中文字與使用之 Unicode

```sh
:%s/\v^(\w*)\t([\u4e00-\u9fff])/\2\t\1/g
```

中文字使用之 Unicode 區間： \u4E00 - \u9FFF

| 字符集       |     字數 | Unicode 編碼 |
| :----------- | -------: | :----------: |
| 基本漢字     | 20902 字 |  4E00-9FA5   |
| 基本漢字補充 |    90 字 |  9FA6-9FFF   |
| 擴展 A       |  6592 字 |  3400-4DBF   |
| 擴展 B       | 42720 字 | 20000-2A6DF  |
| 擴展 C       |  4154 字 | 2A700-2B739  |
| 擴展 D       |   222 字 | 2B740-2B81D  |
| 擴展 E       |  5762 字 | 2B820-2CEA1  |
| 擴展 F       |  7473 字 | 2CEB0-2EBE0  |
| 擴展 G       |  4939 字 | 30000-3134A  |
| 擴展 H       |  4192 字 | 31350-323AF  |
| 康熙部首     |   214 字 |  2F00-2FD5   |
| 部首擴展     | 115 字 ① |  2E80-2EF3   |
| 兼容漢字     | 472 字 ② |  F900-FAD9   |
| 兼容擴展     |   542 字 | 2F800-2FA1D  |
| 漢字筆劃     |    36 字 |  31C0-31E3   |
| 漢字結構     |    12 字 |  2FF0-2FFB   |
| 漢語注音     |    43 字 |  3105-312F   |
| 注音擴展     |    32 字 |  31A0-31BF   |
| 〇           |     1 字 |     3007     |

字數備註:

① 部首擴展：2E9A 是空碼位。 ② 兼容漢字：FA6E、FA6F 是空碼位
。

此頁面的字數按實際字數標示（排除空碼位），編碼範圍則排除了首
尾空碼位。另一個頁面《世界文字大全》的編碼範圍標註則與
Unicode 一致（包括空碼位）。

另，原有 PUA 字符產生於上世紀九十年代，現已全部標準化擁有正
式碼位，故從表中刪除。

Unicode 是全球文字統一編碼。它把世界上的各種文字的每一個字符
指定唯一編碼，實現跨語種、跨平台的應用。

中文用戶最常接觸的是漢字 Unicode 編碼。中文字符數量巨大，日
常使用的漢字數量有數千個，再加上生僻字，數量達到數万個。這個
表格將中文字符集的 Unicode 編碼範圍列出，點擊字庫條目可見具
體字符。若要查詢具體字符的編碼請前往：漢字字符集編碼查詢。
