# time_series_eda_demand_forecast
# 需要予測のための時系列EDA（探索的データ分析）

売上データを例に **時系列データの探索的データ分析（EDA: Exploratory Data Analysis）** を行うサンプルNotebookです。

需要予測モデル（ARIMA / Prophet / 機械学習など）を構築する前に、
データの **トレンド・季節性・曜日効果・自己相関** などを理解することを目的としています。


---

# Notebook

```id="bmx9ie"
time_series_eda_sample.ipynb
```

---

# このNotebookで行うEDA

本Notebookでは以下の分析を行います。

1. ダミー売上データ作成
2. 基本統計量の確認
3. 時系列プロット
4. 移動平均によるトレンド確認
5. 曜日別売上分析
6. 月別売上分析
7. ラグプロット（自己相関の確認）

---

# データについて

このNotebookでは以下の特徴を持つ **ダミー売上データ** を生成しています。

* 売上の長期トレンド
* 週次の季節性
* ランダムノイズ

```python id="r7xt7q"
sales = (
    50
    + 0.2 * np.arange(180)                 # トレンド
    + 10 * np.sin(np.arange(180)/7)        # 週次季節性
    + np.random.normal(0, 3, 180)          # ノイズ
)
```

実際の需要予測データを想定した構造になっています。

---

# 分析内容

## 1 基本統計量

売上データの平均・標準偏差・最大値などを確認します。

```python id="5ocvo1"
df.describe()
```

---

## 2 時系列プロット

売上の時系列推移を可視化します。

確認ポイント

* 長期トレンド
* 季節性
* ノイズ

---

## 3 移動平均

7日移動平均を計算し、売上トレンドを滑らかに表示します。

```python id="yxbm0p"
df["rolling_mean_7"] = df["sales"].rolling(7).mean()
```

移動平均は

* ノイズの除去
* トレンド確認

に役立ちます。

---

## 4 曜日分析

曜日ごとの平均売上を確認します。

```python id="i3f4t0"
df["weekday"] = df.index.dayofweek
```

EC・小売・飲食などのビジネスでは
**曜日による売上の変動（曜日効果）** がよく見られます。

---

## 5 月別売上分析

月ごとの平均売上を可視化します。

```python id="gtblb6"
df["month"] = df.index.month
```

これにより

* 月次の季節性
* 年間トレンド

を確認できます。

---

## 6 ラグプロット（Lag Plot）

ラグ特徴量を作成し、自己相関を確認します。

```python id="7a6ue8"
df["lag1"] = df["sales"].shift(1)
```

ラグプロットでは

* 売上の自己依存性
* 時系列モデルの適用可能性

を確認できます。

---

# 使用ライブラリ

以下のPythonライブラリを使用します。

```id="o6ngri"
pandas
numpy
matplotlib
seaborn
```

インストール

```bash id="tyqf6v"
pip install pandas numpy matplotlib seaborn
```

---

# このNotebookの用途

以下の用途で利用できます。

* 需要予測プロジェクトのEDA
* 売上データ分析
* 時系列分析の学習
* データサイエンスのポートフォリオ

---

# 次のステップ

EDAの次のステップとして、以下の分析を行うことができます。

* ARIMA / SARIMA による需要予測
* Prophet による時系列予測
* 機械学習モデル（XGBoostなど）による予測
* 特徴量エンジニアリング（lag / rolling / holiday）

---

# ライセンス

MIT License
