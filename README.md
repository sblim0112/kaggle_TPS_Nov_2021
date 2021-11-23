### kaggle_TPS_Nov_2021

Optuna를 이용한 LGBM모델 하이퍼 파라미터 튜닝

**LGBM의 주요 Hyperparameters**

1. tree structure 관련
    * max_depth: tree의 level(깊이)을 의미. 값이 높을수록 tree가 복잡해지므로 overfit 가능성 높아짐. 일반적으로 3 ~ 12 가 성능이 좋음
    * num_leaves: terminal nodes의 갯수. max_depth의 범위가 정해졌다면,  $2^{maxdepth}$ 로 하는 것이 좋음
    * min_data_in_leaf: 최종 결정을 위한 최소 데이터 수. training data의 수와 num_leaves와 연관이 있음. 데이터가 크면 100단위나 1000 단위로 하면 됨
    
    
2. 정확도 향상 관련
    * 기본적인 정확도 향상 전략은 tree의 갯수를 늘리고 learning rate를 낮추는 것임
        * 이 경우 학습 속도가 느려지므로 early_stopping_rounds 옵션 적용하여 사용할 것
    * n_estimators: 높을수록 overfitting 가능성 높음
    * learning_rate: 0.01 에서 0.3 사이 정도
    * max_bin: 디폴트인 255 기준으로 더 많이 할 수도 있으나 역시 overfitting 가능성
    
    
3. 과적합 방지 관련
    * lambda_l1: xgboost의 reg_lambda. L1-정규화 패널티항(Lasso 와 같은 기능), 0~100 사이 추천
    * lambda_l2: xgboost의 reg_alpha. L2-정규화 패널티항(Ridge 와 같은 기능), 0~100 사이 추천
    * min_gain_to_split: xgboost의 gamma. 약간 보수적으로 0~15 추천
    * bagging_fraction: 0과 1 사이의 비율값. xgboost의 subsample. 과적합 방지를 위해 해당 비율의 데이터만 학습
    * bagging_freq: 0 이상의 정수 k값. k-th iteration마다 bagging_fraction 만큼의 데이터를 이용하여 bagging 수행
    * feature_fraction: 0과 1 사이의 비율값. xgboost의 colsample_bytree. 개별 tree 학습 시 샘플링할 feature 비율
    * 1번의 max_depth와 num_leaves도 과적합과 관련이 있음
