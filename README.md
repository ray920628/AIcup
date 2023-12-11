# 簡介
本項目是一個使用 EleutherAI 的 Pythia模型進行自然語言處理的示例。它展示了從數據加載、模型訓練、文本生成到結果分析的整個流程。
## 特點
- 使用 Pythia預訓練模型。
- 包含完整的訓練和評估流程。
- 實現了自定義的文本生成。
- 包含數據後處理和分析。
## 安裝環境指南
本指南將幫助您在Google Colab上安裝和配置Python環境，以運行基於Python 3.x的機器學習和自然語言處理腳本。
## 環境需求
* 平台: 推薦使用Google Colab，因為它提供了大量的計算資源。
* Python版本: Python 3.x。
## 設置Python環境
1. 確保您的系統中已安裝Python 3.x。您可以在終端機中運行 `python --version`  來檢查Python版本。
## 安裝依賴項
在您的Colab筆記本中運行以下命令，以安裝所需的庫：

```bash
!pip install transformers
!pip install datasets
```

## 模型選擇
- 如果您是使用Colab的免費GPU，建議您可以使用較小的模型，防止RAM的不足，我使用的是A100的GPU去訓練。
- 這裡可以查看所有的模型，供您選擇 [Pythia Scaling Suite](https://huggingface.co/collections/EleutherAI/pythia-scaling-suite-64fb5dfa8c21ebb3db7ad2e1)

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

plm = "EleutherAI/pythia-410m-deduped" #此處可以修改你想要的模型
bos = '<|endoftext|>'
eos = '<|END|>'
pad = '<|pad|>'
sep ='\n\n####\n\n'

special_tokens_dict = {'eos_token': eos, 'bos_token': bos, 'pad_token': pad, 'sep_token': sep}

tokenizer = AutoTokenizer.from_pretrained(plm, revision="step3000")
num_added_toks = tokenizer.add_special_tokens(special_tokens_dict)
tokenizer.padding_side = 'left'
```

## 資料後處理
主要防止模型產生額外的標籤，並進行刪除，此方法能夠提高分數，可以依照個人需求進行更改。
```python
file_path = '你的answer檔路徑'
train_phi_category = ['PATIENT', 'DOCTOR', 'USERNAME', 'PROFESSION', 'ROOM', 'DEPARTMENT', 'HOSPITAL', 'ORGANIZATION', 'STREET', 'CITY', 'STATE', 'COUNTRY', 'ZIP', 'LOCATION-OTHER', 'AGE', 'DATE', 'TIME', 'DURATION', 'SET', 'PHONE', 'FAX', 'EMAIL', 'URL', 'IPADDR', 'SSN', 'MEDICALRECORD', 'HEALTHPLAN', 'ACCOUNT', 'LICENSE', 'VEHICLE', 'DEVICE', 'BIOID', 'IDNUM']

with open(file_path, 'r', encoding='utf-8') as file:
    lines = file.readlines()

for line_number, line in enumerate(lines, 1):
    label = line.split('\t')[1].strip()
    if label not in train_phi_category:
        print(f"Line {line_number}: {label}")# 獲取不屬於規定標籤，並打印出來
```
```python
file_path = '你的answer檔路徑'
file_path1 = '設定新的answer檔路徑'
train_phi_category = ['PATIENT', 'DOCTOR', 'USERNAME', 'PROFESSION', 'ROOM', 'DEPARTMENT', 'HOSPITAL', 'ORGANIZATION', 'STREET', 'CITY', 'STATE', 'COUNTRY', 'ZIP', 'LOCATION-OTHER', 'AGE', 'DATE', 'TIME', 'DURATION', 'SET', 'PHONE', 'FAX', 'EMAIL', 'URL', 'IPADDR', 'SSN', 'MEDICALRECORD', 'HEALTHPLAN', 'ACCOUNT', 'LICENSE', 'VEHICLE', 'DEVICE', 'BIOID', 'IDNUM']

# 讀取文件並篩選標籤在訓練標籤列表
with open(file_path, 'r', encoding='utf-8') as file:
    lines = file.readlines()

filtered_lines = []
for line in lines:
    label = line.split('\t')[1].strip()
    if label in train_phi_category:
        filtered_lines.append(line)

# 將篩選後重新寫入文件中
with open(file_path1, 'w', encoding='utf-8') as file:
    file.writelines(filtered_lines)
```

## 聯繫方式

如有任何問題，請通過以下郵件地址與我們聯繫：[ray20030628@gmail.com](mailto:ray20030628@gmail.com)。
