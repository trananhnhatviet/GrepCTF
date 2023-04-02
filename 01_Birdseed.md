# **Bird Seed**

-   Challenge này cho ta 2 file là file **encrypt.py** và **out.txt** 

```
#encrypt.py
import random
flag = open('flag.txt').read()

rand_seed = random.randint(0, 999)
random.seed(rand_seed)
encrypted = ''

for chr in flag:
    encrypted += f'{(ord(chr) ^ random.randint(0, 255)):02x}'

with open('out.txt', 'w') as f:
    f.write(encrypted)


#out.txt
a282b415279f5aa08cd4649515268910b8968a1eabda7c1bb2898c
```

-   Ta thấy được rằng, rand_seed được random trong khoảng (0,999). Từ rand_seed này làm căn bản cho bộ sinh số ngẫu nhiên.
-   Tiếp theo, ta thấy đoạn code mã hóa từng ký tự trong "flag" bằng cách thực hiện phép toán XOR giữa mã ASCII của ký tự và một số nguyên ngẫu nhiên trong khoảng từ 0 đến 255, và sau đó chuyển đổi kết quả thành một chuỗi ký tự hexa (dạng chuỗi hexa của một số, có độ dài bằng 2).
-   Thực chất, các số ngẫu nhiên này dựa vào rand_seed để sinh được các số theo bộ sinh số ngẫu nhiên Mersenne Twister, có nghĩa là khi rand_seed là 1 số x, thì bộ sinh số ngẫu nhiên sẽ là 1 dãy số có quy luật
-   Ví dụ rand_seed = 12 thì 10 số được random.randint(0,255) mặc định sẽ là 242, 137, 179, 73, 195, 5, 191, 247, 140, 235
-   Ví dụ rand_seed = 50 thì 10 số được random.randint(0,255) mặc định sẽ là 254, 136, 186, 124, 242, 168, 43, 162, 114, 43

-    Encrypted dưới dạng hexa là 
```
Encrypted = 'a282b415279f5aa08cd4649515268910b8968a1eabda7c1bb2898c'
```
-   Và để dễ hiểu hơn thì ta đổi lần lượt 2 ký tự của Encrypted thành decimal
```
Deci_Encrypted = [162,130,180,21,39,159,90,160,140,212,100,149,21,38,137,16,184,150,138,30,171,218,124,27,178,137,140]
```
-   Bây giờ, ta chỉ cần cho rand_seed trong khoảng (0,999) rồi ta lấy các số được random.randint(0,255) đó XOR lại với Deci_Encrypted là sẽ tìm được flag

-   Đoạn code sẽ như sau:
```
import random

Deci_Encrypted = [162, 130, 180, 21, 39, 159, 90, 160, 140, 212, 100, 149, 21, 38, 137, 16, 184, 150, 138, 30, 171, 218, 124, 27, 178, 137, 140]

for rand_seed in range(0, 999): #Thực ra rand_seed trong khoảng từ 100 --> 500

    random.seed(rand_seed)
    encrypted = ''

    for char in Deci_Encrypted:
        encrypted += chr(char ^ random.randint(0, 255))

    if "grep" in encrypted:
        print(encrypted)

```

***Flag của challenge này là: grepCTF{n3v3r_tru1y_r4nd0m}***
