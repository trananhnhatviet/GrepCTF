# **Derailed**

-   Đề bài: ``You have pwned a Railway website's database. You have the password.txt file which contains the password of their users in the line corresponding to the user ID. An Evil Scientist that goes by the name of Mr. Fence took 4 rails to his different labs. You want to find out his password so that you know where he is headed next. You have to find him fast and apprehend him otherwise the whole world rots. If I tell you his user ID is the 75th prime number - 1, Will You be able to save the world?``

-   Challenge này cho ta file **password.txt** gồm 505 dòng ID :v

-   Ta thấy đề bài có nhắc tới ID của Mr.Fence chính là số nguyên tố thứ 75 trừ đi cho 1 --> Mục tiêu của chúng ta là tìm ra số nguyên tố thứ 75
-   Đoạn code tìm số nguyên tố thứ 75 như sau:
```
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True


def nth_prime_number(n):
    count = 0
    i = 2
    while True:
        if is_prime(i):
            count += 1
        if count == n:
            return i
        i += 1


print(nth_prime_number(75))

```
-   Ta tìm được số nguyên tố thứ 75 là ``379`` --> ID của Mr.Fence là **``378``**

-   Tìm dòng thứ 378, ta thấy được 1 đoạn mã: ``T_OF}ENI_NNfqR{rlQcjeCe_B``
-   Ta thấy tên của nhà khoa học ác đọc là Fence, ta nghĩ ngay tới  ``Rail Fence Cipher Decode``
-   Ngoài ra, ta thấy đề có nói: ``An Evil Scientist that goes by the name of Mr. Fence took 4 rails to his different labs`` --> Key = 4
-   Để decrypt được đoạn mã này, ta vào tools https://gchq.github.io/CyberChef/
-   Tìm Rail Fence Cipher Decode và kéo vào mục Recipe
![](https://i.imgur.com/ucUzOCw.png)
![](https://i.imgur.com/gU50j9m.png)
-   Chọn Key = 4 và nhập đoạn mã ``T_OF}ENI_NNfqR{rlQcjeCe_B`` vào và ta được
![](https://i.imgur.com/93aqfI3.png)
-   Ta thu được đoạn mã ``TERC{N_Irel_ONQ_cNFfjBeq}``
-   Ta sử dụng thêm Caesar Cipher để decrypt đoạn mã này https://www.dcode.fr/caesar-cipher (vì sao mình dùng thì là do tổ tiên mách bảo :v)

-   Nhập đoạn mã vừa thu được và ấn Decrypt(BruteForce), ta thu được ![](https://i.imgur.com/5sDGQgA.png) và flag chính là dòng đầu tiên

***Flag của challenge này là: GREP{A_Very_BAD_pASswOrd}***
