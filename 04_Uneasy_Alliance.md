# **Uneasy Alliance**

-   Challenge này cho ta file **question.py** 

```
from Crypto.Util.number import *
import math
import time
from random import Random

seed = math.floor(time.time())
rnd = Random(seed)

rand_fn = lambda n: long_to_bytes(rnd.getrandbits(n))
p = getPrime(128, randfunc=rand_fn)
q = getPrime(128, randfunc=rand_fn)
e = 65537
n = p * q

assert p != q

m = bytes_to_long(b"GREP{REDACTED}")
ct = pow(m, e, n)
print("Cipher text:", ct)
# Cipher text: 9898717456951148133749957106576029659879736707349710770560950848503614119828
# Seed: REDACTED
```

-   Ta thấy đây chính là mật mã RSA, thế nhưng ta không biết được p và q là gì vì nó là giá trị random dựa trên seed
-  Ta thấy seed = math.floor(time.time()), thế math.floor(time.time()) là gì:
   -  ``math.floor(time.time())`` là lấy giá trị thời gian hiện tại ở định dạng số nguyên bằng cách sử dụng hàm time.time() của module time và làm tròn giá trị đó về phía dưới bằng cách sử dụng hàm math.floor() của module math.

   -  Hàm time.time() trả về số giây từ thời điểm Epoch (00:00:00 UTC, 1 tháng 1 năm 1970) đến thời điểm hiện tại. Giá trị trả về là một số thực có độ chính xác đến micro giây. Bằng cách sử dụng hàm math.floor(), chúng ta làm tròn giá trị đó về phía dưới để được số giây nguyên từ thời điểm Epoch đến thời điểm hiện tại.
-  Thế nên seed sẽ trong khoảng từ 0 tới thời gian hiện tại nên ta sẽ dùng 1 vòng lặp để thử từng giá trị của seed, sau đó sẽ được các giá trị p và q rồi sẽ tìm được flag

-  Đoạn code sẽ như sau:
```
from Crypto.Util.number import *
import math
import time
from random import Random

#Mình cho nó trong khoảng (106700,106715) vì seed chính xác ở trong khoảng đó
for seed in range(106700,106715):
    rnd = Random(seed)

    rand_fn = lambda n: long_to_bytes(rnd.getrandbits(n))
    p = getPrime(128, randfunc=rand_fn)
    q = getPrime(128, randfunc=rand_fn)
    e = 65537
    Cipher=9898717456951148133749957106576029659879736707349710770560950848503614119828
    n = p * q
    phi = (p-1)*(q-1)
    d = inverse(e,phi)
    plain=str(long_to_bytes(pow(Cipher,d,n)))
    if 'GREP' in plain:
        print(plain)
```

***Flag của challenge này là: GREP{Brut3D_M3!_f0r_l1f3}***
