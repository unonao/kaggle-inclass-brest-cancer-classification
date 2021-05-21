# kaggle-inclass-brest-cancer-classification
乳がんの病理生検画像の識別 brest-cancer-classification


# CV
- StratifiedKFold
    - 元々同じ画像から切り出されたものは、同じfoldになるように分けないと正しく検証することができない（例：trainに出現した一個横の画像が検証データに出てくると当てやすい）:GroupKFold
    - 正と負の分布も異なる。GroupKFoldだけだとfold数を大きくとって細かく分けたときに偏りが大きくなる:stratifiedKfold
