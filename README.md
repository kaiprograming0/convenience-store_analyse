# 北陸[石川、富山、福井]+長野のコンビニデータの解析
#### コンビニのデータ解析を通して、店ごとの出店場所の傾向についての把握、立地調査の活用などが挙げられます。

## コード
今回用いたライブラリは以下である。
```python
import pandas as pd
import matplotlib.pyplot as plt
import warnings
import folium
```
### データの読み込み
```python
df = pd.read_csv('ファイル名.csv')
```
### データの前処理
```python
df['列名'].apply(lambda x: x.split('／')[0] if '／' in x else x)
df['列名'].apply(lambda x: '返したい値' if '中に入っている文字' in x else x)
df.loc[df['場所'].str.contains('県名'), '県'] = '県名'
df['店の種類'] = df['店の種類'].apply(lambda x: 'その他' if x not in ['ファミリーマート', 'セブンイレブン', 'ローソン', 'ヤマザキ', 'Yショップ'] else x)
```
### 集計
```python
pd.DataFrame(df['列名'].value_counts())

df[['県', '店の種類', 'カウント']].groupby(['県', '店の種類']).sum().reset_index().sort_values('カウント', ascending=False).head(20)
```

### 円グラフ
```python
plt.pie(df['店の種類'].value_counts(), labels=df['店の種類'].value_counts().index, startangle=90, autopct='%1.1f%%')

categories = df['店の種類'].unique()
colors_dict = {'石川': 'orange', '長野': 'blue', '富山': 'green', '福井': 'red'}

fig, axes = plt.subplots(2, 3, figsize=(10, 8))
axes = axes.flatten()

for i, category in enumerate(categories):
    data_subset = df[df['店の種類'] == category]['県'].value_counts()
    sorted_data = dict(sorted(data_subset.items(), key=lambda item: item[1], reverse=True))
    
    axes[i].pie(sorted_data.values(), labels=sorted_data.keys(), autopct='%1.1f%%', startangle=90, counterclock=False)
    axes[i].set_title(f'{category}県別分布')
    
plt.tight_layout()
plt.show()
```




