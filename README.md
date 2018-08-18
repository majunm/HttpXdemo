#### 请求三部曲


> 请求体
```
//http://www.wanandroid.com/user/register ||等效接口
@ReqTags("注册")
public class RegisterReq extends CommonRequest {
    public String username;
    public String password;
    public String repassword;

    public RegisterReq(String username, String password, String repassword) {
        this.username = username;
        this.password = password;
        this.repassword = repassword;
    }

    public RegisterReq() {
    }

    @Override
    public String postfix() {
        return "user/register";
    }
}


```

> 响应体
```
public class RegisterResp implements Data {
    public String email;
    public String icon;
    public int id;
    public String password;
    public int type;
    public String username;
    //collectIds // what 暂时不写

    @Override
    public String toString() {
        return "RegisterResp{" +
                "email='" + email + '\'' +
                ", icon='" + icon + '\'' +
                ", id=" + id +
                ", password='" + password + '\'' +
                ", type=" + type +
                ", username='" + username + '\'' +
                "} " + super.toString();
    }
}
```

| 发起请求

```
 final RegisterReq json = new RegisterReq("12132322333", "123456", "123456");
 final IProgressDialog iLoading = createLoading();
 HttpRequestFactory.doPost(json, new ResultCallbackAdapt<HttpCommObjResp<RegisterResp>>() {
            @Override
            public void doOnResponse(HttpCommObjResp<RegisterResp> response) {
                System.out.println(response + "");
                mContent.setText("\n方式一返回:" + response);
            }

            @Override
            public void doOnError(ApiException ex) {
                System.out.println(ex + "");
                mContent.setText("\n方式一返回:" + ex);
            }
        }, iLoading);
```