# **Wan Wan Wan**


-   Challenge này cho ta file **doge.py** 

```
from Crypto.Util.number import *
from pwn import xor
flag = b'REDACTED'
key = b'REDACTED'
enc = b''
for i in range(len(flag)):
    enc += xor(key[i], flag[i])
print(enc)
# enc = b'#="5\x07\x1b\x01>4#s<u! \x1a3~3-\x1b7w7\x1b&4\x1a":)8'
```
-  Ta thấy đề cho ``FLAG FORMAT: grepCTF{...}``, tức là trong flag sẽ có dạng là grepCTF{XXX...XXX}
-  Challenge còn cho ta 1 đoạn bytes ``enc = b'#="5\x07\x1b\x01>4#s<u! \x1a3~3-\x1b7w7\x1b&4\x1a":)8'`` và chuyển qua hex ta được đoạn hexa như sau
```
hex_enc = '233d2235071b013e3423733c7521201a337e332d1b3777371b26341a223a2938'
```
-  Vì mình thích nên mình chuyển qua decimal :v
```
dec_enc=[35,61,34,53,7,27,1,62,52,35,115,60,117,33,32,26,51,126,51,45,27,55,119,55,27,38,52,26,34,58,41,56]

```
-  Đặt 1 biến là ``flag_demo = 'grepCTF{'``
-  Đặt 1 list 8 phần tử tương đương với flag_demo là 8 phần tử đầu của dec_enc: ``demo_dec_enc = [35,61,34,53,7,27,1,62]``
-  Mục tiêu bây giờ là cần tìm được demo_Key là gì
-  demo_Key sẽ bằng từng phần tử của flag_demo Xor lần lượt với từng phần tử demo_dec_enc, tức là ``demo_Key[i] = xor(flag_demo[i],demo_dec_enc[i])``
-  Đoạn code sẽ như sau:
```
flag_demo = 'grepCTF{'
demo_dec_enc = [35,61,34,53,7,27,1,62]
demo_Key=""
for i in range(len(flag_demo)):
    demo_Key += (xor(flag_demo[i],demo_dec_enc[i])).decode()
print(demo_Key)
```
-  Khi đó, ``demo_Key = 'DOGEDOGE'``. Không chỉ thế, ta thấy len(dec_enc) = 32 --> Ta đoán ``Key = 'DOGEDOGEDOGEDOGEDOGEDOGEDOGEDOGE'``

-  Có Key rồi, ta tìm flag bằng cách tương tự khi ta tìm demo_Key ``flag[i] = xor(Key[i],dec_enc[i])``
-  Đoạn code sẽ như sau:
```
from pwn import xor

Key = 'DOGEDOGEDOGEDOGEDOGEDOGEDOGEDOGE'

flag = ""

dec_enc = [35, 61, 34, 53, 7, 27, 1, 62, 52, 35, 115, 60, 117, 33, 32, 26, 51, 126, 51, 45, 27, 55, 119, 55, 27, 38, 52, 26, 34, 58, 41, 56]


for i in range(len(Key)):
    flag = flag+str(xor(Key[i], (dec_enc[i])).decode())

print(flag)

```

***Flag của challenge này là: grepCTF{pl4y1ng_w1th_x0r_is_fun}***
