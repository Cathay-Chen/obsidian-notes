 ---
##  ParseInt
```go
// 参数1 数字的字符串形式  
// 参数2 数字字符串的进制 比如二进制 八进制 十进制 十六进制  
// 参数3 返回结果的 bit 大小也就是 int8 int16 int32 int64
func ParseInt (s string, base int, bitSize int) (i int64, err error)  
```

---
## 升级 go 
```shell
brew update
brew upgrade go
```

---
## base64

 [base64 编解码](http://zh.wikipedia.org/wiki/Base64)
```go
data := "abc123!?$*&()'-=@~"

// Go 同时支持标准 base64 以及 URL 兼容 base64。 
// 这是使用标准编码器进行编码的方法。 
// 编码器需要一个 `[]byte`，因此我们将 string 转换为该类型。
sEnc := b64.StdEncoding.EncodeToString([]byte(data))
fmt.Println(sEnc) // YWJjMTIzIT8kKiYoKSctPUB+

// 解码可能会返回错误，
// 如果不确定输入信息格式是否正确， 
// 那么，你就需要进行错误检查了。
sDec, _ := b64.StdEncoding.DecodeString(sEnc)
fmt.Println(string(sDec)) // abc123!?$*&()'-=@~
fmt.Println()

// 使用 URL base64 格式进行编解码。
uEnc := b64.URLEncoding.EncodeToString([]byte(data))
fmt.Println(uEnc) // YWJjMTIzIT8kKiYoKSctPUB-
uDec, _ := b64.URLEncoding.DecodeString(uEnc)
fmt.Println(string(uDec)) // abc123!?$*&()'-=@~
```

---
## Urlencode

[How to perform URL decoding in Golang](https://www.urldecoder.io/golang/)

```go
fmt.Println(url.QueryEscape(query))

params := url.Values{}
params.Add("name", "@Rajeev")
params.Add("phone", "+919999999999")

fmt.Println(params.Encode())

path := "path with?reserved+characters"
fmt.Println(url.PathEscape(path))
```

---

## 简单的 Http 服务代码

```go
func startHttp(port int) {  
   port1 := strconv.Itoa(port)  
   if port1 == "" {  
      common.Error("web端口错误")  
      return  
   }  
  
   http.HandleFunc("/healthcheck", func(writer http.ResponseWriter, request *http.Request) {  
      writer.Header().Set("Content-Type", "application/json")  
      writer.WriteHeader(200)  
      encoder := json.NewEncoder(writer)  
      var response struct {  
         State uint        `json:"state"`  
         Data  interface{} `json:"data"`  
         Msg   string      `json:"msg"`  
      }  
      response.State = 200  
      response.Msg = "success"  
  
      if err := encoder.Encode(response); err != nil {  
         http.Error(writer, err.Error(), 500)  
      }  
   })  
  
   common.Info("http listen start", port1)  
  
   if err := http.ListenAndServe(":"+port1, nil); err != nil {  
      common.Error("http listen err", err)  
   }  
}
```


## [[GO 语言中的锁]]
