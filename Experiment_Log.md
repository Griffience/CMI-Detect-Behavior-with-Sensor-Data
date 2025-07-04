# Exp log

## **exp1**
| 步骤         | Baseline（双分支 NN）        | 改造后（IMU-only 树模型）                                 |
| ---------- | ----------------------- | ------------------------------------------------- |
| ① **特征工程** | 去重力、角速度、角距离等 **同样保留**   | **保留**（只做 IMU 部分）                                 |
| ② **序列处理** | **pad 到固定 `T`** → 3D 张量 | **聚合到 1 行**<br>对每个特征取 *mean/std/min/max/…*        |
| ③ **模型**   | CNN+RNN+Attention       | LightGBM / XGBoost / CatBoost / TabNet…           |
| ④ **交叉验证** | `train_test_split`      | `StratifiedGroupKFold(n_splits=5, group=subject)` |
| ⑤ **调参**   | 手写超参                    | **Optuna** 自动搜索                                   |
| ⑥ **推理**   | `predict()`→pad→模型      | `predict()`→同样聚合→ `.predict_proba()`              |
