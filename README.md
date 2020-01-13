# SuperSQL3DVS(デモ・実験用)
## 概要
本システムはSuperSQLとUnityとを組み合わせて, 簡潔なクエリ記述のみで3次元空間にデータ可視化を可能とする.  
SuperSQLについては[SuperSQL](https://github.com/ToyamaLab/NewSSQL)を参照.  

＊今回はデモ用のものなので, 事前にSuperSQLクエリから作成されたファイルを用いたデータ可視化を体験するものとなっている.

[アンケートページ](https://forms.gle/WKw6FJcDCpmy923z9)

## 導入手順
- 本システムの導入
 1. 右上のgit Clone or Downloadボタンからダウンロード
 1. zipファイルを解凍
 1. Unity Hubを開き、プロジェクトからリストに追加を選択
 1. ダウンロードしてきたプロジェクト(ディレクトリ)を開く(DataVisualization-master)
 1. 追加したプロジェクトを開く(最初は開くまでに時間がかかります。おやつを用意して気長にお待ちください)
 <img width="722" alt="スクリーンショット 2020-01-08 19 18 54" src="https://user-images.githubusercontent.com/25918044/71970310-c8bd3300-324b-11ea-853a-7fe9edc8b86a.png">

- 起動
 1. Unityの画面が開いたら、▷(スタート)ボタンをクリックで開始
 <img width="866" alt="スクリーンショット 2020-01-08 19 22 21" src="https://user-images.githubusercontent.com/25918044/71970561-45e8a800-324c-11ea-9ba5-5d3cc485655b.png">

## 作業手順
最初に数分, 一通りの操作を実行して感覚を掴んでください。操作説明は次に示してあります。
[アンケートページ](https://forms.gle/WKw6FJcDCpmy923z9)を開き, 問題を解くたびにアンケートに結果を記入してください。


## 操作説明  
**移動**  
キーボードの矢印で移動。  
- ↑ y軸正の方向に移動
- ↓ y軸負の方向に移動
- → x軸正の方向に移動
- ← x軸負の方向に移動
- RightCommand or RightControl + ↑ z軸正の方向に移動
- RightCommand or RightControl + ↓ z軸負の方向に移動  
上記 + 右Shiftで移動が少し速くなる。

**回転**  
- 矢印+LeftCommand or LeftControlでカメラが回転
- LeftCommand or LeftControl + → y軸中心に時計回りに回転
- LeftCommand or LeftControl + ← y軸中心に反時計回りに回転
- LeftCommand or LeftControl + ↑ x軸中心に時計回りに回転
- LeftCommand or LeftControl + ↓ x軸中心に反時計回りに回転

**詳細表示**  
- LeftCommand or LeftControl + オブジェクトにカーソルを重ねると詳細が表示されます
<img width="581" alt="スクリーンショット 2020-01-13 16 17 09" src="https://user-images.githubusercontent.com/25918044/72238221-810a2300-3620-11ea-83eb-002cb516d3a0.png">  
**シーン遷移**  
- クエリでscene関数がついているゲームオブジェクトをクリックすると, シーンが遷移します

**フィルタリング, カメラボタン + 問題一覧**
- 画面右上プルダウンをクリックすると, フィルターとカメラボタンが利用できます。questionsを押すと, 10個の問題が見えます。
<img width="889" alt="スクリーンショット 2020-01-08 18 35 09" src="https://user-images.githubusercontent.com/25918044/71966866-b50ece00-3245-11ea-8b66-93b978690523.png">

## クエリ説明  
- データ割り当て  
	大きさ: 人口, 色: 気温, 風車の回転: 風力
- 人口が多いほど大きい, 色が青いほど気温が低く、赤いほど気温が高い, 回転が早いほど風力が強い
- クエリ2, 3ではオブジェクトクリックするとクエリ4(wind.ssql)にシーン遷移する

＊データは実験用の物です。実際の情報とは異なる物なのでご了承下さい。

## クエリ1(basic.ssql)
```
[null((asc)c.year),Object("text", c.year || "年", 10),
	[null((asc)c.month),Object("text", c.month || "月", 10),
		[null((asc)c.day),Object("text", c.day || "日", 10),
			[null(c.name),
				color_gradient(
					rotate(
						asset("Windmill", c.population/5000), 0, 0, c.wind * 10
					)@{target="Fan"}, "blue", min[c.temperature], "red", max[c.temperature], c.temperature
				)! Object("text",c.name,10)
			],@{margin = 50}
		]%@{margin = 100}
	]!@{margin = 300}
]%@{margin = 300}
```

## クエリ2(rayout.ssql)
```
------時間配置------
[null(c.name),
	[null((asc)c.day),Object("text", c.day || "日", 10),
		color_gradient(
			rotate(
				scene(
						asset("Windmill", c.population/5000), "wind", c.id
				), 0, 0, c.wind * 10
			)@{target="Fan"} ,"blue", max[c.temperature], "red", max[c.temperature], c.temperature
		)
	]#
		!Object("text",c.name,10)
],
------時間配置------
,
------円配置------
[null(c.name),
	[null((asc)c.day),
		color_gradient(
				scene(
					object("sphere", c.population/5000), "wind", c.id
				), "blue", min[c.temperature], "red", max[c.temperature], c.temperature
		)
	]◯
	!object("text", c.name, 50)
]%@{margin=200}
------円配置------
,
------日本地図配置------
[null((asc)c.day),
	[position({move(object("text", c.day || "日", 10), c.longitude*80 -5030, c.day * 300, c.latitude*80),
			move(
				move({object("text", c.name, 5)
					!
					color_gradient(
						move(
							rotate(
								scene(
									asset("Windmill", c.population/5000), "wind", c.id
								), 0, 0, c.wind * 10
							)@{target="Fan"}, 0, c.population/5000, 0
						), "blue",min[c.temperature],"red",max[c.temperature],c.temperature
					)}, 0, c.day * 300, 0
				), c.longitude * 80 - 5000, 0, c.latitude * 80
		)}, 0, 0, 0
	)]!
]%
------日本地図配置------
from cities c 
where c.year = 2018 and c.month = 8
```

## クエリ3(filter.ssql)
```
[null((asc)c.day),Object("text", c.day || "日", 10),
	[null(c.name),
		color_gradient(
			rotate(
				filter(
					filter(
						scene(
							asset("Windmill", c.population/5000), "wind", c.id
						), c.wind@{name="wind"}, "slider"
					), c.temperature@{name="temperature"}, "slider"
				), 0, 0, c.wind * 10
			)@{target="Fan"}, "blue", min[c.temperature], "red", max[c.temperature], c.temperature
		)!Object("text",c.name,10)
	],@{margin = 50}
]%@{margin=100}
```

## クエリ4(wind.ssql)
```
foreach c.id
generate Unity_dv
[null((asc)c.year),Object("text", c.year || "年", 10),
	[null((asc)c.month),Object("text", c.month || "月", 10), 
		[null((asc)c.day), Object("text", c.day || "日", 10), 
			color_gradient(
				rotate(asset("Windmill", c.population/5000), 0, 0, c.wind * 10)@{target="Fan"},
				"blue", min[c.temperature], "red", max[c.temperature], c.temperature
			)
		],
	]!
	!Object("text",c.name,10)
]%@{margin=200}
from cities c 
```
