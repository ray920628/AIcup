# 安裝環境指南
本指南將幫助您在Google Colab上安裝和配置Python環境，以運行基於Python 3.x的機器學習和自然語言處理腳本。
## 環境需求
* 平台: 推薦使用Google Colab，因為它提供了大量的計算資源。
* Python版本: Python 3.x。
## 設置Python環境
1. 確保您的系統中已安裝Python 3.x。您可以在終端機中運行 `python --version`  來檢查Python版本
。
## 安裝依賴項
在您的Colab筆記本中運行以下命令，以安裝所需的庫：

```bash
!pip install transformers
!pip install datasets
```

## Usage

```python
import foobar

# returns 'words'
foobar.pluralize('word')

# returns 'geese'
foobar.pluralize('goose')

# returns 'phenomenon'
foobar.singularize('phenomena')
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
