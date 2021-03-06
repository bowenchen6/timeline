## 在Heroku上部署发布Golang程序
1. 在github上创建项目，例如go-retwis-heroku，初始化README，添加gitignore，license等文件。
2. 使用go get工具，下载项目到本地的GOPATH开发环境中，例如：

        go get github.com/yourname/go-retwis-heroku/...

3. 出现错误是正常的，因为当前没有golang的代码，添加一个简单的Hello World的代码, 例如：

        package main

        import (
        	"fmt"
        	"log"
        	"net/http"
        	"os"

        	"github.com/urfave/negroni"
        )

        func main() {
        	port := os.Getenv("PORT")

        	if port == "" {
        		log.Fatal("$PORT must be set")
        	}

        	mux := http.NewServeMux()
        	mux.HandleFunc("/", func(w http.ResponseWriter, req *http.Request) {
        		fmt.Fprintf(w, "Hello World!")
        	})

        	n := negroni.Classic() // Includes some default middlewares
        	n.UseHandler(mux)
        	n.Run(":"+port)
        }

4. 添加Procfile的文本文件，需要包含web字段，这样Heroku才会做路由处理，内容可以如下：

        web: go-retwis-heroku

5. 使用Godep管理项目依赖，使用命令来生成：

        go get github.com/tools/godep
        godep save ./...

6. 下载Heroku CLI工具，并安装，然后在命令行输入heroku login命令登录到Heroku。
7. 使用heroku create命令来创建应用。
8. 使用git push heroku master命令来部署我们的程序。

        git add .
        git commit -m 'init your project'
        git push　//提交代码到github
        git push heroku master

9. 如果部署成功，可以使用heroku open打开我们Hello World网站。

10. 可以添加.env文件，并添加环境变量PORT：

        PORT=8080

11. 这样可以在本地运行命令启动程序

        go install
        heroku local

12. 可以添加额外组件如pg, redis等来做更有意义的事情，添加额外组件的命令：

        heroku addons:create heroku-redis

13. 实例网站：　https://go-retwis.herokuapp.com/　实例代码：　https://github.com/bowenchen6/go-retwis-heroku
