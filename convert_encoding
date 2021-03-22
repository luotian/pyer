#!/usr/bin/python3

import os
import sys
import chardet
import codecs

# 当前脚本路径
rootpath = os.path.dirname(os.path.abspath(sys.argv[0]))
print("Exec ConverCode RootDir: ", rootpath)

# 目标编码
dst_coding = "utf-8"

# 是否有效的文件
def IsValidFile(filename):
    if (filename.endswith(".h") 
        or filename.endswith(".cpp")  
        or filename.endswith(".cc")):
        return True
    return False

# 重写文件
def WriteFile(filePath, content, encode):
    with codecs.open(filePath, "w", encode) as f:
        f.write(content)

# 转码
def ConvertCode(src, dst):
    f = open(src, "rb")
    detect_val = chardet.detect(f.read())
    coding = detect_val["encoding"]
    f.close()
    if coding != dst_coding:
        with codecs.open(src, "r", coding) as f:
            try:
                WriteFile(dst, f.read(), dst_coding)
                try:
                    print(src + "  " + coding + " to " + dst_coding + " converted!")
                except Exception:
                    print("print error")
            except Exception:
                print(src +"  "+ coding+ "  read error")

# 读取所有符合条件的文件
def ReadAllFileRecure(rootdir):
    for parent, _, filenames in os.walk(rootdir):
        for filename in filenames:
            #print("Filename:" + os.path.join(parent, filename))
            if IsValidFile(filename):
                ConvertCode(os.path.join(parent, filename),
                        os.path.join(parent, filename))

if __name__ == "__main__":
    ReadAllFileRecure(rootpath)
