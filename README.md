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
 1. - Mac: 解凍したディレクトリ(DataVisualize-master)内のSuperSQL3DVS_for_Macを一度別のディレクトリに移動して, 同じディレクトリ内に戻してください。(これをしないと, ssql.propertiesを読み込んでくれません)  
 その後, SuperSQL3DVS_for_Macを実行(ダブルクリック)  
 - Windows: SuperSQL3DVS_for_Winディレクトリ内のNew Unity Project.exeを実行(ダブルクリック)  
注意がでるので、すべて展開を選択  
展開終了後, NewUnityProject.exeをダブルクリック 
 <img width="609" alt="スクリーンショット 2020-01-13 16 34 53" src="https://user-images.githubusercontent.com/25918044/72239066-173f4880-3623-11ea-94ae-888c02e9cb67.png">
 1. config画面が開くので, 設定してPlay!ボタンをクリックで開始されます(おすすめ Resolution: 1152*720, Graphics: Low)  
 <img width="481" alt="スクリーンショット 2020-01-13 16 44 07" src="https://user-images.githubusercontent.com/25918044/72239456-7a7daa80-3624-11ea-8438-c57e137085d9.png">

*終了ボタンがないので, WindowsはAlt+F4で終了してください.

## 作業手順
最初に数分, 一通りの操作を実行して感覚を掴んでください。操作説明は次節に示します。  
[アンケートページ](https://forms.gle/WKw6FJcDCpmy923z9)を開き, 問題を解くたびにアンケートに結果を記入してください。  
### 手順1  
- 右上のプルダウンでQuestionを選択 → Question1~10が表示される
- Question1を選択する → 問題とタイマーが表示される
- 準備ができたらStartを押して, 探索を開始
- 答えが分かった時点でStopを押し, アンケートページへ
<img width="885" alt="スクリーンショット 2020-01-13 16 59 58" src="https://user-images.githubusercontent.com/25918044/72240037-34294b00-3626-11ea-8a7e-1c3f368bd7ae.png">  
- アンケートに答えと表示されている時間を記入
<img width="801" alt="スクリーンショット 2020-01-13 17 04 10" src="https://user-images.githubusercontent.com/25918044/72240210-c7628080-3626-11ea-9da2-f4f81ef11b84.png">  
- Question2を選択  
- 準備ができたらStartを押す(Startを押すと自動でタイマーはリセットされます)  
- これをQuestion10まで行う。  
### 手順2  
 次に別のシーンを使用する.
 - ssql.propertiesを開き, basic.xml -> rayout.xmlに書き換えて保存
 <img width="610" alt="スクリーンショット 2020-01-13 17 21 59" src="https://user-images.githubusercontent.com/25918044/72241181-83bd4600-3629-11ea-8f38-3417743136f7.png">  
 - SuperSQL3DVS_for_Macを起動(起動に数十秒かかります. 少々お待ちください)

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
- データに関して
地名には東京をのぞいた, 46道府県の県庁所在地が入っている.
風力, 気温は日付や市によって値が変わるが, 人口はどの日付でも同じ値(市によってのみ値が異なる). 

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
