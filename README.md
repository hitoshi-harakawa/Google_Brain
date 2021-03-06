# Google_Brain
## 2021/10/11開始
- Discription(訳: DeepL)
  
  患者が呼吸困難に陥ったとき、医師は何をするのだろうか。人工呼吸器を使って、鎮静状態の患者の肺に気管から酸素を送り込むのだ。しかし、人工呼吸は臨床医の手が必要であり、その限界はCOVID-19パンデミックの初期に顕著に現れました。同時に、機械式人工呼吸器を制御する新しい方法を開発するには、臨床試験に至るまでに莫大な費用がかかります。高品質のシミュレーターは、この障壁を軽減することができます。
  
  Google Brainのチームは、プリンストン大学と提携し、機械的な人工呼吸の制御のための機械学習に関するコミュニティの拡大を目指しています。ニューラルネットワークと深層学習は、現在の業界標準であるPID制御よりも、さまざまな特性を持つ肺をよりよく一般化できると考えています。
  
  このコンペティションでは、鎮静状態の患者の肺に接続された人工呼吸器をシミュレートします。優れた作品は、肺の属性であるコンプライアンスと抵抗を考慮しています。
  
  成功すれば、機械式人工呼吸器を制御する新しい方法を開発する際のコストの壁を乗り越えることができます。これにより、患者に適応したアルゴリズムへの道が開かれ、この斬新な時代とそれ以降の時代において、臨床医の負担を軽減することができます。その結果、患者さんの呼吸を助けるための人工呼吸器の治療法がより広く普及することになるかもしれません。
  
- Evaluation(訳: DeepL)

  競技は、各呼吸の吸気段階における予測圧力と実際の圧力の間の平均絶対誤差として採点される。呼気相は採点されない。スコアは次のように与えられる。
  
  |𝑋-𝑌|
  
  ここで、𝑋は予測圧力のベクトルであり、𝑌はテストセットの全呼吸における実際の圧力のベクトルである。

- Dataset
  
  train.csvが8カラム、test.csvが7カラムとカラム数が少ない。
  
  本大会で使用した人工呼吸器のデータは、オープンソースの人工呼吸器を改造し、呼吸回路を介して人工蛇腹試験肺に接続して作成しました。下図はその設定を示したもので、2つの制御入力を緑で、予測する状態変数（気道圧）を青で示しています。1つ目の制御入力は，0〜100の連続変数で，空気を肺に入れるために吸気電磁弁を開く割合を表します（すなわち，0は完全に閉じて空気を入れず，100は完全に開きます）。2つ目の制御入力は、空気を出すための探索電磁弁が開いている（1）か閉じている（0）かを表す二値変数です。

  この競技では，参加者に多数の呼吸の時系列が与えられ，制御入力の時系列が与えられた場合に，呼吸時の呼吸回路内の気道圧力を予測することを学習する．
  
  各時系列は、約3秒間の呼吸を表しています。ファイルは、各行が呼吸のタイムステップとなるように構成されており、後述する2つの制御信号、その結果としての気道圧力、および肺の関連属性を示しています。

<img width="917" alt="スクリーンショット 2021-10-11 22 54 30" src="https://user-images.githubusercontent.com/68815430/136804215-637fc413-38ee-4d29-ba1a-cd4d693f15e3.png">

カラム

id - ファイル全体でグローバルに一意のタイムステップ識別子

breath_id - グローバルに一意な呼吸のタイムステップ

R - 気道がどの程度制限されているかを示す肺属性（単位：cmH2O/L/S）。物理的には、流量（時間当たりの空気量）の変化に対する圧力の変化です。直感的には、ストローで風船を膨らませるようなイメージです。ストローの直径を変えることでRを変化させることができ、Rが大きいほど吹きにくくなります。

C - 肺の適合性を示す肺属性（単位：mL/cmH2O）。物理的には、圧力の変化に対する体積の変化を表します。直感的には、同じ風船の例を想像してください。風船のラテックスの厚さを変えることでCを変化させることができます。Cが大きいほどラテックスが薄く、吹きやすくなります。

time_step - 実際のタイムスタンプです。

u_in - 吸気ソレノイドバルブの制御入力です。0～100の範囲で設定できます。

u_out - 探索用ソレノイドバルブの制御入力です。0または1のいずれかです。

pressure - 呼吸回路で測定された気道圧力で、単位はcmH2Oです。


## 10/12
kaggleの進め方記事

https://qiita.com/shu421/items/ed255c1ad846c92ba448
https://qiita.com/Java_is_a_sparrow/items/b4f4dd4a2c4530db5a72

- discassion, notebookを全て読む
- 時間をかける

EDA

https://www.kaggle.com/marutama/eda-about-lstm-feature-importance
- LSTMとは→https://qiita.com/KojiOhki/items/89cd7b69a8a6239d67ca
