# RC4原理概述
## 1.先初始化一个S向量，256字节，每个值都是下标
## 2.再通过我们自己设定的密钥，轮转生成256字节的T向量
## 3.再将j=0;j=(j+S[i]+T[i])的j为下标，进行S向量的交换，打乱S向量
## 4.接下来就是生成密钥流，
```
   // 生成密钥流
    int i,j;
    int temp, t, k;
    int index = 0;
    i = j = 0;
    while(textLength --){   //生成密钥流
        i = (i+1)%256;
        j = (j + S[i]) % 256;
        temp = S[i];
        S[i] = S[j];
        S[j] = temp;
        t = (S[i] + S[j]) % 256;
        KeyStream[index] = S[t];
        index ++;
    }
```
## 5.然后就是明文逐位的和密钥流进行异或，这就是序列密码(流密码的操作)，这意味着，只要密钥流一样，那么密文经过相同加密过程，反而变成了解密，23333