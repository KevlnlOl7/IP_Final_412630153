# 影像處理_期末專案說明
## 布匹缺陷偵測
> **組員**：412630153 張傢寧 ( 組長 )、412631508 許方彥 
> **授課老師**：陳建彰 老師

---

## 資源下載中心

這裡彙整了本專案的所有檔案，請點擊連結進行檢閱或下載。

| 項目 | 說明 | 連結 |
| :--- | :--- | :--- |
| **📄 簡報投影片** | 要上台報告用的 | [[點此開啟 Canva]](https://www.canva.com/design/DAG9fH_083I/I-qSOpebCSF7rvnonCPW_w/view?utm_content=DAG9fH_083I&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hb0cd794084) |
| **🎥 成果展示影片(框起來版)** | 瑕疵偵測後的輸出結果 | [[點此觀看 YouTube](https://www.youtube.com/watch?v=V0AUhxipFrM)] |
| **🎥 成果展示影片(填滿缺陷版)** | 瑕疵偵測後的輸出結果 | [[點此觀看 YouTube]](https://youtu.be/9LCOLxVUY7g) |
| **🗣️ 專題解說影片** | 3分鐘重點功能與程式碼解說 | [[點此觀看 YouTube](https://youtu.be/uTLwXROz3AE)] |
| **⚖️ 模型權重檔** | 包含 EfficientNet-B7 等 4 個模型 (.pth) | [[點此下載 (Hugging Face)]](https://huggingface.co/creadaillfly/IP_Final_412630153/tree/main) |
| **💻 原始程式碼** | 包含 .ipynb 與 requirements.txt | [[點此下載 / GitHub 連結]](https://github.com/KevlnlOl7/IP_Final_412630153/tree/main) |

---

## 使用說明

### 模型權重
首先要請老師先點開上方 `模型權重檔` 的連結下載模型權重檔
![image](https://hackmd.io/_uploads/rJ2vXfOVWg.png)
點開網址後，依序點選第二至第六個 (requirements.txt) 中間的下載按鈕。
下載完後，請將四個權重檔移至專案根目錄
![image](https://hackmd.io/_uploads/BJcm7fO4-e.png)

### Juypeter NoteBook 設定
！！！ 請確保電腦已安裝 NVIDIA 顯卡驅動程式！！！
打開 Juypeter NoteBook 後，先建立新的終端機，並進入 requirements.txt 所在位置
接著輸入 `pip install -r requirements.txt` 將所需檔案都下載下來

接著移動到環境變數的部分
```text!
IMAGE_PATH = "老師隱藏測資的圖片位置"  # 輸入影像路徑
GT_PATH = "老師隱藏測資的 groundtruth 位置"  # 標準答案路徑
OUTPUT_PATH = "模型預測輸出的位置"  # 預測結果路徑
SAVE_PATH = "模型預測與老師 groundtruth 的比較圖" # 比較圖的輸出
```
再來是模型設定的部分，若老師跟我一樣是放在專案根目錄的話就複製貼上即可
```text!
MODELS_CONFIG = [
        {"arch": "UnetPlusPlus", "encoder": "timm-efficientnet-b7", "path": "best_S2_B7_Plus.pth", "weight": 1.2},
        {"arch": "UnetPlusPlus", "encoder": "densenet161", "path": "best_The_Detail_Dense161.pth", "weight": 1.0},
        {"arch": "UnetPlusPlus", "encoder": "resnet101", "path": "best_S3_Res101.pth", "weight": 1.0},
        {"arch": "UnetPlusPlus", "encoder": "efficientnet-b5", "path": "best_S2_B5.pth", "weight": 0.8},
]
```
然後中文字體、模型載入設定以及 main() 方法，都不需要特別去設定，直接按執行即可
要特別注意的一點是，若評估結果那邊顯示...，有高機率是被折疊，我用 VSCode 測試有遇到這個問題，但 PyCharm 則不會

接下來是影片區域我弄了兩個版本，一個是圈起來的版本，另一個是填滿的版本
兩者要調的參數是一樣的
```text!
INPUT_VIDEO_PATH = 'Data/texture_video_1.avi'  # 輸入影片
OUTPUT_VIDEO_PATH = 'test.mp4'  # 輸出影片
DEVICE = torch.device('cuda')
```
模型設置的部分亦同
```text!
MODELS_CONFIG = [
    {"arch": "UnetPlusPlus", "encoder": "timm-efficientnet-b7", "path": "best_S2_B7_Plus.pth", "weight": 1.2},
    {"arch": "UnetPlusPlus", "encoder": "densenet161", "path": "best_The_Detail_Dense161.pth", "weight": 1.0},
    {"arch": "UnetPlusPlus", "encoder": "resnet101", "path": "best_S3_Res101.pth", "weight": 1.0},
    {"arch": "UnetPlusPlus", "encoder": "efficientnet-b5", "path": "best_S2_B5.pth", "weight": 0.8},
]


IMG_HEIGHT = 512
IMG_WIDTH = 512
FINAL_THRESHOLD = 0.5
```
圈起來版 VS 填滿版

圈起來版
![image](https://hackmd.io/_uploads/BJBJbX_4Zl.png)

填滿版
![image](https://hackmd.io/_uploads/SkbtWQdN-e.png)
