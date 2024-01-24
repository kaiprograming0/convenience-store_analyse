# 北陸[石川、富山、福井]+長野のコンビニデータの解析
#### コンビニのデータ解析を通して、店ごとの出店場所の傾向についての把握、立地調査の活用などが挙げられます。

## コード
今回用いたライブラリは以下である。
```
import pandas as pd
import matplotlib.pyplot as plt
import warnings
import folium
```
### データの読み込み
```
df = = pd.read_csv('ファイル名.csv')
```
### データの前処理
```
df['列名'].apply(lambda x: x.split('／')[0] if '／' in x else x)
df['列名'].apply(lambda x: '返したい値' if '中に入っている文字' in x else x)
df.loc[df['場所'].str.contains('県名'), '県'] = '県名'
```



