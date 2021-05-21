# kaggle-inclass-brest-cancer-classification
乳がんの病理生検画像の識別 brest-cancer-classification


# 要約
- StratifiedGroupKFoldでちゃんとCVを切る
    - StratifiedKFold   CV:0.91480, public:0.87397, private:0.87369
    - GroupKFold    CV:0.90991, public:0.87175, private:0.87413
    - StratifiedGroupKFold     CV:0.86842 (出してないけどpublicとprivateはそんなに変わらないはず。かなりCVスコアが安定した)
- モデルは dm_nfnet_f0
    -  tf_efficientnet_b1    CV:0.86842
    -  dm_nfnet_f0    CV:0.87642, public:0.88645, private:0.88816
- 【重要】50x50 の画像だと情報量が少なすぎ。周辺のパッチを含めて 3x3 枚使って 150x150 のサイズで学習
    - fold3→fold5についでに変更。CV:0.91820, public:0.91018, private:0.91016
- 最後に周辺パッチ3x3の予測値を特徴量として lightgbmで学習（スタッキング）
    - CV:0.92732, public:0.91296, private:0.91441

# CVについてもう少し
- StratifiedGroupKFoldで安定的なCV
    - 元々同じ画像から切り出されたものは、同じfoldになるように分けないと正しく検証することができない（例：trainに出現した一個横の画像が検証データに出てくると当てやすい）:GroupKFold
    - 正と負の分布も異なる。GroupKFoldだけだとfold数を大きくとって細かく分けたときに偏りが大きくなる:stratifiedKfold
