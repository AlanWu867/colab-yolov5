# colab-yolov5訓練
[yolo下載與安裝環境](#首先下載yolov5檔案)

[建立數據集](#建立數據集)

[產生訓練需要的資源](#產生訓練需要的資源)

[建立colab Terminal](#建立colab_Terminal)

[訓練與測試](#訓練與測試)
## yolo下載與安裝環境
下載檔案到google drive(推薦)或是指令git clone直接下載，但重新啟動要再下一次指令。
```
$ git clone https://github.com/ultralytics/yolov5
$ cd yolov5
$ pip install -r requirements.txt
```
## 建立自己所需數據集
### 1. 方案1
   - [labelImg](https://tzutalin.github.io/labelImg/)
   - 在目錄yolov5/data底下建立Annotations與JPEGImages資料夾，分別存放.xml標註檔與圖片
### 2. 方案2
   - 下載已標籤的開放數據集，如：[VOC2007](https://www.kaggle.com/zaraks/pascal-voc-2007)
   - 透過pascalVOC_to_voc.py挑取所需的類別(詳細步驟---->[來源](https://makerpro.cc/2020/01/get-specific-objects-from-voc-dataset/))
   - 由於pascalVOC_to_voc.py會將pose加入名稱內如果不希望加入可以使用上方檔案voc_to_voc
## 產生訓練需要的資源
   - 詳細步驟---->[YOLOV5训练自己的数据集（踩坑经验之谈）](https://blog.csdn.net/a_cheng_/article/details/111401500)
## 建立colab_Terminal
   - 程式來源---->[How can I run shell (terminal) in Google Colab?](https://stackoverflow.com/questions/59318692/how-can-i-run-shell-terminal-in-google-colab)
### 1. 啟動shell
```python
from IPython.display import JSON
from google.colab import output
from subprocess import getoutput
import os

def shell(command):
  if command.startswith('cd'):
    path = command.strip().split(maxsplit=1)[1]
    os.chdir(path)
    return JSON([''])
  return JSON([getoutput(command)])
output.register_callback('shell', shell)
```
### 2. 顯示Terminal(Colab Shell)
```python
#@title Colab Shell
%%html
<div id=term_demo></div>
<script src="https://code.jquery.com/jquery-latest.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery.terminal/js/jquery.terminal.min.js"></script>
<link href="https://cdn.jsdelivr.net/npm/jquery.terminal/css/jquery.terminal.min.css" rel="stylesheet"/>
<script>
  $('#term_demo').terminal(async function(command) {
      if (command !== '') {
          try {
              let res = await google.colab.kernel.invokeFunction('shell', [command])
              let out = res.data['application/json'][0]
              this.echo(new String(out))
          } catch(e) {
              this.error(new String(e));
          }
      } else {
          this.echo('');
      }
  }, {
      greetings: 'Welcome to Colab Shell',
      name: 'colab_demo',
      height: 250,
      prompt: 'colab > '
  });
```
## 訓練與測試
### 1. 訓練
```
python train.py --data class_name.yaml --cfg yolov5s.yaml --weights weights/yolov5s.pt --epochs 10 --batch-size 32
```
### 2. 測試
```
python detect.py --weights runs/train/exp1/weights/best.pt --source data/Samples/ --device 0 --save-txt
```
