## 一、设置单元格格式

有时我们利用python修改excel时需要单元格具有特殊格式，如字体格式、居中设置等，对此在实践中我采用两种简单的方法：

### 方法一：预设excel模板，利用openpyxl直接写入
这个方法试用下来在多数场景下最实用，先设置一个设定好格式的excel模板文件，再利用openpyxl包修改已有的excel模板，能直接继承模板设置好的格式，如下：

```python
    from openpyxl import load_workbook
    #adress是模板的位置
    address=r'.\test.xlsx'
    workbook = load_workbook(filename=address)
    sheet = workbook.active
    sheet["A1"] = 'test1'
    workbook.save(filename=address)
    workbook.close()
```

但是由于未知原因，有极少数时候直接写入后格式会变，这时我们可以采用第二种方法

### 方法二：利用openpyxl.styles包修改格式

具体如下：

```python
from openpyxl import load_workbook
from openpyxl.styles import Alignment
from openpyxl.styles import Font
\#单元格格式设置
ali=Alignment(
    horizontal='center',  # 水平对齐，可选general、left、center、right、fill、justify、centerContinuous、distributed
    vertical='top',  # 垂直对齐， 可选top、center、bottom、justify、distributed
    text_rotation=0,  # 字体旋转，0~180整数
    wrap_text=True,  # 是否自动换行
    shrink_to_fit=False,  # 是否缩小字体填充
    indent=0,  # 缩进值
)
\#单元格字体设置
font = Font(
    name="Arial",   # 字体
    size=9,         # 字体大小
    color="000000",  # 字体颜色，用16进制rgb表示
    bold=False,       # 是否加粗，True/False
    italic=False,     # 是否斜体，True/False
    strike=None,     # 是否使用删除线，True/False
    underline=None,  # 下划线, 可选'singleAccounting', 'double', 'single', 'doubleAccounting'
)
address=r'.\test.xlsx'
workbook = load_workbook(filename=address)
sheet = workbook.active
sheet['A1'].alignment = ali
sheet['A1'].font = font
workbook.save(filename=address)
workbook.close()
```

***

## 二、调整列宽

利用openpyxl包内置功能即可

```python
from openpyxl import load_workbook
address=r'.\test.xlsx'
wb = load_workbook(address)
ws = wb.active
\# 调整列宽
ws.column_dimensions['A'].width = 3.5
ws.column_dimensions['B'].width = 3.5
ws.column_dimensions['C'].width = 14.63
ws.column_dimensions['D'].width = 45.38
ws.column_dimensions['E'].width = 4.75
ws.column_dimensions['F'].width = 5.5
wb.save(filename=address)
wb.close()
```



***

自用笔记 ，如有疑问，欢迎讨论