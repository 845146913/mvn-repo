# mvn-repo

#### 介绍
MAVEN个人仓库

#### 使用说明

1.  MAVEN
``` java
<repositories>
    <repository>
        <id>silencew-maven</id>
        <url>https://gitee.com/wangshuip/mvn-repo/raw/master</url>
    </repository>
    <repository>
        <id>silencew-repository</id>
        <url>https://raw.github.com/845146913/mvn-repo/master</url>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </snapshots>
    </repository>
</repositories>



<dependency>
    <groupId>com.silencew.plugins</groupId>
    <artifactId>jpa-enums-plugin</artifactId>
    <version>1.0.5</version>
</dependency>

<!--请求参数自定义枚举插件starter-->
<dependency>
    <groupId>com.silencew.plugins</groupId>
    <artifactId>silencew-enums-spring-boot-starter</artifactId>
    <version>1.0.5</version>
</dependency>
```
## silencew-enums-starter升级至1.0.5
> BaseEnum codeOf优化，添加codeOfOptional方法，不再默认抛出非法参数异常
> requestBody 解析json枚举字段移除解析失败抛出异常代码，交给validation等框架扩展 
## enum-jackson插件说明20220611

原来jpa-enums-plugin的starter插件更名为enum-jackson-boot-starter；

对应版本为1.0-SNAPSHOT，稳定版本为1.0.1；
```html
<dependency>
    <groupId>com.silencew.plugins</groupId>
    <artifactId>enum-jackson-boot-starter</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>

<!--推荐使用release版本-->
<dependency>
    <groupId>com.silencew.plugins</groupId>
    <artifactId>enum-jackson-boot-starter</artifactId>
    <version>1.0.1</version>
</dependency>
```

## enum-swagger3插件说明
基于springfox3.0扩展的自定义枚举展示插件；支持自定义枚举解析和原始枚举类解析；
可配置enum-jackson插件一起使用；
使用示例：
```html
<!--// pom.xml引入依赖-->
<dependency>
    <groupId>com.silencew.plugins</groupId>
    <artifactId>enum-swagger3</artifactId>
    <version>1.0.1</version>
</dependency>
```
```java

@Getter
@AllArgsConstructor
@SwaggerEnum
public enum WindowType implements BaseEnum<WindowType, Integer> {
    DOS(1),
    LINUX(2);
    private final Integer code;
}
// or 原始enum
@Getter
@AllArgsConstructor
@SwaggerEnum
public enum WindowType {
    DOS(1, "windows"),
    LINUX(2, "ubuntu");
    private final Integer code;
    private final String message;
    @JsonValue
    public Integer getCode() {
        return this.code;
    }
}

@Data
@ApiModel("测试模型")
public class DemoDto {
    @ApiModelProperty("返回码")
    private int code;
    @ApiModelProperty("标识")
    private boolean flag;
    @ApiModelProperty("标识1")
    private String name;
    @ApiModelProperty("类型")
    private WindowType type;
}
@RestController
public class TestController{
    @PostMapping
    @ApiOperation("test2")
    public Object test1(@RequestBody DemoDto req) {
        return ResponseEntity.ok(req);
    }
}
```

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  Gitee 官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解 Gitee 上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是 Gitee 最有价值开源项目，是综合评定出的优秀开源项目
5.  Gitee 官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  Gitee 封面人物是一档用来展示 Gitee 会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
