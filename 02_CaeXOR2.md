# **CaeXOR2**

**Bài này khá giống với CaeXOR1 nên mình chỉ giải 1 bài thui nhaa <3**

-   Challenge này cho ta file **enc.py** 

```
#enc.py
from random import *
flag="REDACTED"
a=randint(1,1000)
c=[]
for f in flag:
   c.append(str(ord(f)^a))
print(c)
print(a)

#c=['313', '296', '295', '304', '274', '280', '263', '280', '263', '310', '315', '310', '316', '345', '268', '263', '310', '302', '345', '296', '276']
#a=REDACTED
```

-   Ta thấy a là 1 số ngẫu nhiên trong khoảng (1,1000) và sau đó Xor với với từng các giá trị decimal của các ký tự trong flag và rồi cho vào list c
-   Và challenge cho ta 1 list c gồm các ký tự string (thực chất là các số), nên hãy xóa các dấu ' để nó thành list các số 
```
c=[313, 296, 295, 304, 274, 280, 263, 280, 263, 310, 315, 310, 316, 345, 268, 263, 310, 302, 345, 296, 276]
```
-   Sau đó, ta cho a chạy trong khoảng (1,1000), rồi ta Xor với các phần tử của list c
```
for a in range(0,1000):
   s=""
   for i in c:
      s=s+chr(i^a)
```

-   Đoạn code sẽ như sau:
```
from random import *

c=[313, 296, 295, 304, 274, 280, 263, 280, 263, 310, 315, 310, 316, 345, 268, 263, 310, 302, 345, 296, 276]
for a in range(0,1000):
   s=""
   for i in c:
      s=s+chr(i^a)
   print(s,a)

```

-   Sau đó, ta thấy nó in ra được 1000 dòng gồm là giá trị của s tương ứng với giá trị của a
![](https://i.imgur.com/lQg1f2p.png)
-   Ta thấy ở dòng 361, có 1 đoạn rất giống form flag ``PANY{qnqn_R_U0en_G0A}`` 
-   Nhìn kỹ đề bài, ta thấy là CaeXor2, qua đó, ta cần sử dụng Caesar cipher để decrypt 1 lần nữa
-   Vào https://www.dcode.fr/caesar-cipher rồi nhập ``PANY{qnqn_R_U0en_G0A}`` rồi chọn Decrypt(Bruteforce)
![](https://i.imgur.com/ZEKP1xk.png)

-   Ta thấy dòng đầu tiên là ``GREP{hehe_I_L0ve_X0R}
`` chính là flag của bài

***Flag của challenge này là: GREP{hehe_I_L0ve_X0R}***
