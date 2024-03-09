# william
import datetime
import os
import pandas as pd
import numpy as np

def SP_read(path):
    # 搜索词报告
    df1 = pd.read_excel(path, sheet_name='商品推广 搜索词展示量份额 报告')

    return [df1]
#设置目录

path='/Users/blobeats/Desktop/搜索词展示量份额报告'

def process_search_term_report(path):
    """
    读取指定路径的搜索词报告Excel文件，按广告组合名称分组，
    并为每个组合名称生成一个以“广告组合名称搜索词报告.xlsx”为文件名的Excel文件。
    """
    try:
        df = pd.read_excel(path)
    except FileNotFoundError:
        print(f"文件未找到: {path}")
        return
    except Exception as e:
        print(f"读取文件时出错: {e}")
        return

    # 检查列名是否正确，这里假设正确的列名为"广告组合名称"
    grouped = df.groupby('广告组合名称')

    for name, group in grouped:
        file_name = f"{name}SP-STR.xlsx".replace('/', '_').replace('\\', '_')
        # 修改路径为动态路径
        output_path = os.path.join('/Users/blobeats/Desktop/搜索词展示量份额报告', file_name)
        try:
            group.to_excel(output_path, index=False)
            print(f"文件已成功导出：{output_path}")
        except Exception as e:
            print(f"导出文件时出错: {e}")
