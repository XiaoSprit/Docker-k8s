# API 安全策略
nginx+lua 限制ip和频次
## 开发API存在的安全问题 
- 数据窃取 窃取用户密码信息，获敏感信息、盗刷
- 数据篡改 提交的数据被抓包(钓鱼)篡改后再提交
- 数据泄露 爬虫抓取业务数据造成直接或间接损失

## 如何让API不再裸奔
- RAS、DES 用公、私钥、

### 加、解密算法
DES 对称加密：对于相同的明文进行多次加密，每次加密结果都一样(给了彩虹表存在空间) 使用同一个SK

RAS 非对称加密： 对于相同的明文进行多次加密,每次加密结果都不一样 公钥加密 私钥解密
特点： 
1. 非对称加密，即：PK与SK不是同一个

2. PK用于加密，SK用于解密

3. PK决定SK，但是PK很难算出SK（数学原理：两个大质数相乘，积很难因式分解）

4. 速度慢，只对少量数据加密

AES：Advanced Encrytion Standard（高级加密标准）
    特点：1. 对称加密 2. 一个SK扩展成多个子SK，轮加密

### MD5混淆 防止数据篡改
客户端与服务端约定一个salt(盐)对上传参数进行混淆 
客户端->{
    上传参数->{
        orderId:10086,
        amount:1
    }->加密上传
}

### 防爬虫
Token令牌防爬虫

Base64是一种编码格式