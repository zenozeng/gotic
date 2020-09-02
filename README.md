你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# gotic
Converts files files into go code.

# Concept
Gotic is both, a library and an utility.
The library `gotic/fs`wraps `ioutil.ReadFile()`.
The utility, `gotic`, takes one or more files and genaraates go code representing
them (as one or more `[]byte{ ... }`)

# Install

`go get github.com/zenozeng/gotic` OR `go get ./...`

# Usage

Let's say you have a program (`main.go`) that reads af file:

```go
package main

import "github.com/gchaincl/gotic/fs"

func main() {
  f, err := fs.ReadFile("some/file")
  if err != nil {
    panic(err)
  }
  
  println(string(f))
}

```

Now, to embed `some/file` into your code, just run:
```bash
$ gotic some/file > main_gotic.go
```

Generated `main_gotic.go` will look like:

```go
package main

import "github.com/gchaincl/gotic/fs"

func init() {
	fs.Add("some/file", []byte{ "\xff\xd8\xff\xe1 ..." })
}
```

That's all, as gotic has `Add`ed `some/file`, each call to `fs.ReadFile()`, will return the embedded `[]byte`
instead of actually read the file.
