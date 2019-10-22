SpringBoot搭建SSM工程

接着上一讲，我们已经初步搭建好了springboot的启动工程，那如何将springboot与前端工程，与后端工程mybatis结合呢？这是我们今天需要探讨的问题

1，与前端工程整合

1.1 搭建controller控制层

```java
@RestController("test")
public class TestController {

    @GetMapping("/hello")
    public String hello ()
    {
        return "hello world";
    }

    @GetMapping("getSuccess")
    public AjaxResult getSuccess()
    {
        return new AjaxResult().success("党已经注意到了你的声音");
    }
    
    @PostMapping("postData")
    public AjaxResult postData()
    {
        return new AjaxResult().error("请求失败了，请重试");
    }

}
```

