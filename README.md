# blog
simple
# blog
- 首页
	- [我的博客首页]
- 查看
        - [显示所有文章]](#all_list)

- 添加  
         - [添加文章]](#add)

	
- 搜索
	- [根据输入的内容搜索](#search_list)
	
- 删除
	- [根据ID删除文章](#delete)
	
- 查看
	- [根据ID查看文章](#look)
	- [可进入修改文章] (#edit)
- View
首页->我的博客url localhost:8080/article/home
- controller  
- 路由器通过获得的URL地址  - [router.go]  (#router)   router.GET("/article/home", GetAll)
- 获得方法GetAll() 
- func GetAll(c *gin.Context) {
-	// var articles []Article
-
-	articles := GetAllArticle()
-	c.HTML(http.StatusOK, "home.html", gin.H{
-		"title":   "首页",
-		"Article": articles,
-	})
-
-}
-调用moldels的getAllArticle方法获取，数据库中Article数据，由C.html渲染页面并传送数据，完成首页的查看所有文章
-Moldels
-调用models.GetAllArticle()

-func GetAllArticle() (article []*Article) {
-	article = make([]*Article, 0) //Xorm表名
-	err := db.Orm.Find(&article)
-	if err != nil {
-		//错不为空，就是错了！
-		log.Fatal(err.Error())
-		return nil
-	}
-	return article
-}

   





-router.go 内容

-package routers

-import (
-	. "blog/controllers"
-	"github.com/gin-gonic/gin"
-)
-
-func InitRouter() *gin.Engine {
-	router := gin.Default()
-	// router.Static("/static", "./static")
-	router.LoadHTMLGlob("views/*")
-	router.GET("/article/home", GetAll)
-	// router.GET("/article/:id", GetArticle)
-	router.GET("/article/addhtml", AddHtml)
-	router.POST("/article/add", Add)
-	router.GET("/article/delete", Delete)
-	router.GET("/article/look", Look)
-	router.GET("/article/editHtml", EditHtml)
-	router.POST("/article/edit", Edit)
-	router.POST("/article/search", Search)
-	// router.GET("article/edit", Edit)
-	return router
- }
	




- 拼接参数：
- Article 表

- type Article struct {
-	Id int64 `json:"id" form:"id" xorm:"not null pk INT(11)"`
-	//``反引号 是个tag
-	Title       string    `json:"title" form:"title"`
-	Content     string    `json:"content" form:"content"`
-	Createdtime time.Time `json:"createdtime" form:"createdtime" xorm:"TIME"`
-}
-
- id	    id 值
- title	    文章名字
- content	    文章内容
- createdtime 创建时间
