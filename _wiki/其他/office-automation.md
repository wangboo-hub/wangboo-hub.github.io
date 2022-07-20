---
title: office-automation
authors: admin
priority: 7.18
---

#  office-automation by Python

## PDF

Python 操作 PDF 会用到两个库，分别是：PyPDF2 和 pdfplumber

-  **PyPDF2** 可以更好的读取、写入、分割、合并PDF文件，
-  **pdfplumber** 可以更好的读取 PDF 文件中内容和提取 PDF 中的表格

> :point_right:[PyPDF2网站](https://pypi.org/project/PyPDF2/) 
> 
> :point_right:[pdfplumber网站](https://pypi.org/project/pdfplumber/) 

### PDF拆分
将一个完整的 PDF 拆分成几个小的 PDF，因为主要涉及到 PDF 整体的操作，使用 PyPDF2 库。

#### 按照指定间隔全部拆分
拆分的大概思路如下：

- 读取 PDF 的整体信息、总页数等
- 遍历每一页内容，以每个 step 为间隔将 PDF 存成每一个小的文件块
- 将小的文件块重新保存为新的 PDF 文件

需要注意的是，在拆分的过程中，可以手动设置间隔，

例如：每5页保存成一个小的 PDF 文件

拆分的代码如下：

```python
import os
from PyPDF2 import PdfFileWriter, PdfFileReader

def split_pdf(filename, filepath, save_dirpath, step=5):
    """
    拆分PDF为多个小的PDF文件，
    @param filename:文件名
    @param filepath:文件路径
    @param save_dirpath:保存小的PDF的文件路径
    @param step: 每step间隔的页面生成一个文件，例如step=5，表示0-4页、5-9页...为一个文件
    @return:
    """
    if not os.path.exists(save_dirpath):
        os.mkdir(save_dirpath)
    pdf_reader = PdfFileReader(filepath)
    # 读取每一页的数据
    pages = pdf_reader.getNumPages()
    for page in range(0, pages, step):
        pdf_writer = PdfFileWriter()
        # 拆分pdf，每 step 页的拆分为一个文件
        for index in range(page, page+step):
            if index < pages:
                pdf_writer.addPage(pdf_reader.getPage(index))
        # 保存拆分后的小文件
        save_path = os.path.join(save_dirpath, filename+str(int(page/step)+1)+'.pdf')
        print(save_path)
        with open(save_path, "wb") as out:
            pdf_writer.write(out)

    print("文件已成功拆分，保存路径为："+save_dirpath)
    
filename = 'myfilename' # 替换为拆分待文件的文件名，包括文件后缀.pdf
filepath = os.path.join(os.getcwd(), filename)
save_dirpath = os.path.join(os.getcwd(), 'mysaveddir') # 存放新文件的文件夹，若放在当前文件夹下，则为空
split_pdf(filename, filepath, save_dirpath, step=5)
```

#### 按照指定部分拆分
拆分的大概思路如下：

根据输入的拆分页面要求：“start-end” 进行拆分，可以选取多个连续页面。

拆分的代码如下：

```python
def check_page_list(s):
    for i in range(1, len(s) - 1):
        if s[i] not in ['-', ',', ' ', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9']:
            return True
    return False


def split_pdf(filename, filepath, save_dirpaths, listmode):
    # 使用PDF包中的方法，读取PDF文件
    """
    拆分PDF为多个小的PDF文件，
    @param filename:文件名
    @param filepath:文件路径
    @param save_dirpath:保存小的PDF的文件路径
    @return:
    """
    if not os.path.exists(save_dirpath):
        os.mkdir(save_dirpath)
    pdf_reader = PdfFileReader(filepath)
    pages = pdf_reader.getNumPages()

    try:
        if check_page_list(listmode):
            raise ValueError
        else:
            # 根据用户输入，按‘,’切分输入
            pdf_writer = PdfFileWriter()
            part =listmode.split(',')
            # 遍历每一段“start-end”

            for k in part:
                start,end = k.split('-')
                # 对于范围内的页面，提取出写入新的PDF文件
                for m in range(int(start) - 1, int(end)):
                    page = pdf_reader.getPage(m)
                    pdf_writer.addPage(page)

            save_path = os.path.join(save_dirpath, filename.split('.')[0]+'page'+listmode+'.pdf')
            print(save_path)
            with open(save_path, "wb") as out:
                pdf_writer.write(out)
    except:
        print('拆分范围输入错误，请检查输入格式')

    else:    
        print("文件已成功拆分，保存路径为："+save_dirpath)

s='start-end' # 输入拆分范围，格式为‘start-end’，例如‘1-6,14-16’
filename = 'myfilename' # 替换为拆分待文件的文件名，包括文件后缀.pdf
filepath = os.path.join(os.getcwd(), filename)
save_dirpath = os.path.join(os.getcwd(), 'mysaveddir') # 存放新文件的文件夹，若放在当前文件夹下，则为空
split_pdf(filename, filepath, save_dirpath, s)
```

### PDF合并

比起拆分来，合并的思路更加简单：

- 确定要合并的 **文件顺序**
- 循环追加到一个文件块中
- 保存成一个新的文件

对应的代码比较简单，基本不会出现问题：

```python
import os
from PyPDF2 import PdfFileReader, PdfFileWriter

def concat_pdf(list_filename,read_dirpath, save_filepath):
    """
    合并多个PDF文件
    @param list_filename:待合并的文件名列表
    @param read_dirpath:要合并的PDF目录
    @param save_filepath:合并后的PDF文件路径
    @return:
    """
    pdf_writer = PdfFileWriter()
    for filename in list_filename:
        print(filename)
        filepath = os.path.join(read_dirpath, filename)
        # 读取文件并获取文件的页数
        pdf_reader = PdfFileReader(filepath)
        pages = pdf_reader.getNumPages()
        # 逐页添加
        for page in range(pages):
            pdf_writer.addPage(pdf_reader.getPage(page))
    # 保存合并后的文件
    with open(save_filepath, "wb") as out:
        pdf_writer.write(out)
    print("文件已成功合并，保存路径为："+save_filepath)

#将待合并的文件放入当前文件夹下的一个文件夹里，这里替换改文件夹的名称
read_dirpath = os.path.join(os.getcwd(), 'filedir') 
save_filepath = os.path.join(os.getcwd(), 'mergedfilename') # 替换为合并后的文件名
# list_filename = ['file1','file2','file3'] # 为指定合并顺序，手动添加待合并文件的文件名
list_filename = os.listdir(read_dirpath) # 直接读取整个文件夹，无法指定顺序
# list_filename.sort() # 若文件名称有序号，可以读取整个文件夹后排序
print(list_filename)
concat_pdf(list_filename, read_dirpath, save_filepath)
```

