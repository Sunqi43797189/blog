---
title: Golang加密
date: 2020-06-12 17:02:59
tags:
  - Golang
categories:
  - Golang
---

### HmacSHA1加密

```go
key := []byte(key)
mac := hmac.New(sha1.New, key)
mac.Write([]byte(content))
data := mac.Sum(nil)
```

### MD5

```go
md5Ctx := md5.New()
md5Ctx.Write(dataByte)
cipherStr := md5Ctx.Sum(nil)

//md5后转为16进制字符串 b59c67bf196a4758191e42f76670ceba
hex.EncodeToString(cipherStr)
md5str := fmt.Sprintf("%x", cipherStr)

//或者写入方式换一下
w := md5.New()
io.WriteString(w, str)
md5str := fmt.Sprintf("%x", w.Sum(nil))
return md5str
```



### Base64编码

```go
base64Md5Str := base64.StdEncoding.EncodeToString(Str) // 编码
base64.StdEncoding.DecodeString(data) // 解码
```
