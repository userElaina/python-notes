[toc]
#### 常量
```py
def pt(a:all)->None:
	print(repr(a))

pt(pt)
pt(pt.__name__)
pt(pt.__code__)
pt(pt.__code__.co_argcount)
# <function pt at 0x0000[数据删除(8位hex)]6160>
# 'pt'
# <code object pt at 0x0000[数据删除(8位hex)]5710, file "c:\[数据删除]\1.py", line 28>
# 1
```
```py
import sys
markfunc=lambda:print('Func: '+sys._getframe().f_code.co_name)
def f123():
	exec('print(\'Func: \'+sys._getframe().f_code.co_name)')
	print('Func: '+sys._getframe().f_code.co_name)
	markfunc()
f123()
# Func: <module>
# Func: f123
# Func: <lambda>
print('Func: '+sys._getframe().f_code.co_name)
# Func: <module>
```

#### dict
```py
a={'a':11,'b':22}
a.setdefault('a',33)
a.setdefault('c',44)
print(a)
print(list(a.keys()))
print(list(a.values()))
print(list(a.items()))
# {'a': 11, 'b': 22, 'c': 44}
# ['a', 'b', 'c']
# [11, 22, 44]
# [('a', 11), ('b', 22), ('c', 44)]
a={'a':11,'b':22}
b={'a':33,'c':44}
a.update(b)
print(a)
# {'a': 33, 'b': 22, 'c': 44}
a={'a':11,'b':22}
b={'a':33,'c':44}
for i in a:
	b.setdefault(i,a[i])
print(b)
# {'a': 33, 'c': 44, 'b': 22}
```

#### 16进制字符串
```py
a=0x0ffff
pt(a)
#65535
a=hex(a)
pt(a)
#'0xffff'
a=int(a,16)
pt(a)
#65535
a='0x%06x'%a
pt(a)
#'0x00ffff'
```

#### QrCode
```py
from MyQR import myqr
# version:
# 	28~ 6pts
# 	21~27 5pts
# 	14~20 4pts
# 	13~07 3pts
# 	06~01 2pts
myqr.run(
    words='https://qr.alipay.com/fkx115182a0hebsywxykzb4?t=1615869550701',
	# words='wxp://f2f07MalVJ8TbM6cD-7GvSMUFLfQY1Sk4nq3',
	# 扫描二维码后，显示的内容，或是跳转的链接
    version=13,
	# 设置容错率
    level='H',
	# 控制纠错水平，范围是L、M、Q、H，从左到右依次升高
    picture='D:\\bg.gif',
	# 图片所在目录，可以是gif
    colorized=True,
	# 黑白(False)/彩色(True)
    contrast=1.0,
	# 用以调节图片的对比度。默认1.0，表示原始图片。
    brightness=1.0,
	# 用来调节图片的亮度。默认1.0，表示原始图片。
    save_name='D:\\alipay3.png'
	# 控制输出文件名，格式 [jpg,png,bmp,gif]
)
```

#### unvcode
```py
def from_unvcode():
	d=dict()
	ans=0
	for i in range(0x0000,0x10000):
	# 就这个范围的文字有 unvcode
		字 = chr(i)
		新字 = unicodedata.normalize('NFKC', 字)
		if 字 != 新字:
			ans+=1
			if 新字 in d:
				d[新字].append(字)
			else:
				d[新字]=[字]
	print(ans)

	s=''
	for i in d:
		s+=i+'\t'+'\t'.join(d[i])+'\n'
	f=open('_unvcode.txt','wb').write(s.encode('utf-8'))
语言范围={
	'jp':[0x3040,0x3100],
	'ch':[0x4e00,0xa000]
}
```

#### 新建空白图片
(2105,1487)为A4纸
##### cv2
```py
import numpy as np
import cv2
img=np.zeros((2105,1487,3),np.uint8)
img.fill(255)
cv2.imshow('image_cv2',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
cv2.imwrite('cv2.png',img)
```
##### PIL
```py
from PIL import Image
img=Image.new('RGB',(2105,1487),0xffffff)
img.show()
img.save('pil.png')
```

