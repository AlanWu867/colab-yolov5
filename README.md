# colab-yolov5訓練
[yolo下載與安裝環境](##首先下載yolov5檔案)

## yolo下載與安裝環境
下載檔案到google drive(推薦)或是指令git clone直接下載，但重新啟動要再下一次指令。
```
$ git clone https://github.com/ultralytics/yolov5
$ cd yolov5
$ pip install -r requirements.txt
```
## 建立數據及
### 1. 方案1
   - [labelImg](https://tzutalin.github.io/labelImg/)
   - 在目錄yolov5/data底下建立Annotations與JPEGImages資料夾，分別存放.xml標註檔與圖片
### 2. 方案2
   - 下載已標籤的開放數據集
   - 透過pascalVOC_to_voc.py挑取所需的類別(詳細步驟---->[來源](https://makerpro.cc/2020/01/get-specific-objects-from-voc-dataset/))
   - 由於pascalVOC_to_voc.py會將pose加入名稱內如果不希望加入可以使用上方檔案voc_to_voc
