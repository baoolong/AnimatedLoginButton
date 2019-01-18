# AnimatedLoginButton

[![pub package](https://img.shields.io/pub/v/animatedloginbutton.svg)](https://pub.dartlang.org/packages/animatedloginbutton)

双平台通用,使用简单，动画炫酷，可自定义大小尺寸等，如果使用当中有什么问题，请在github里提出个issues,thankYou

It is a good widget,can compatible with Android and IOS,Adjustable progress,Customizable color and size,
If there is any problem with the use, please submit an issue in github,thankYou

#### My organization's github：[https://github.com/OpenFlutter](https://github.com/OpenFlutter)

#### Contact Me ：OpenFlutter QQ群 892398530

<img width="38%" height="38%" src="https://raw.githubusercontent.com/baoolong/PullToRefresh/master/demonstrationgif/20181127_165032.gif"/>

## Usage

Add this to your package's pubspec.yaml file:

    dependencies:
	  animatedloginbutton: "^0.1.1"

Add it to your dart file:

    import 'package:animatedloginbutton/animatedloginbutton.dart';

## Example
    
    import 'dart:io';
    import 'dart:convert';
    import 'package:flutter/material.dart';
    import 'package:animatedloginbutton/animatedloginbutton.dart';
    
    class LoginAnimationDemo extends StatefulWidget{
    
      @override
      State<StatefulWidget> createState() {
        return new LoginAnimationDemoState();
      }
    
    }
    
    class LoginAnimationDemoState extends State<LoginAnimationDemo>{
    
      //使用系统的请求
      var httpClient = new HttpClient();
      var url = "https://github.com/";
      var _result="";
      final LoginErrorMessageController loginErrorMessageController=LoginErrorMessageController();
    
      @override
      void initState() {
        super.initState();
      }
    
    
      @override
      Widget build(BuildContext context) {
    
        return new Scaffold(
          appBar: new AppBar(
            title: new Text("登陆按钮动画"),
          ),
          body: new Center(
            child:new Container(
              child:new AnimatedLoginButton(
                loginErrorMessageController:loginErrorMessageController,
                onTap: () async {
                  try {
                    var request = await httpClient.getUrl(Uri.parse(url));
                    var response = await request.close();
                    if (response.statusCode == HttpStatus.ok) {
                      _result = await response.transform(utf8.decoder).join();
    
                      //拿到数据后，对数据进行梳理
                      loginErrorMessageController.showErrorMessage("网络异常");
    
                    } else {
                      _result = 'ERROR CODE: ${response.statusCode}';
                      loginErrorMessageController.showErrorMessage("网络异常 $_result");
                    }
                  } catch (exception) {
                    _result = '网络异常';
                    loginErrorMessageController.showErrorMessage("网络异常");
                  }
                  print(_result);
                },
              ),
            ),
          ),
        );
      }
    }
    
## Properties

| properties                    | type              | description                                                           |
| ----                          | ----              | ----                                                                  |
| loginTip                      | String            |   登陆按钮提示 Login button prompt    	                                |
| width                         | double      		|   button的宽度 Button width	                                        |
| height                        | double      		|   button的高度 Button Height   			                            |
| indicatorStarRadian           | double      	    |   弧形指标器的起始角度（旋转的那个带箭头的东西）  The starting angle of the curved indicator (the one with the arrow that rotates)  |
| indicatorWidth                | double      		|   指标器的宽度  Indicator width   	                                    |
| buttonColorNormal             | Color      		|   未登陆时Button的颜色  Button color when not logged in	                |
| buttonColorError              | Color      		|   登陆异常Button的颜色    Button color when Login failed  			    |
| indicatorColor                | Color      		|   指标器的颜色  Indicator color	                                        |
| textStyleNormal               | TextStyle      	|   未登录时Button文字的样式   Style of text when not logged in	        |
| textStyleError                | TextStyle         |   登陆异常时Button文字的样式  The style of the text when the login fails |
| onTap                         | typedef           |   点击事件  Click event 	|
| loginErrorMessageController   | LoginErrorMessageController  |   用来显示异常信息  Used to display exception information 	|
| showErrorTime                 | Duration          |   异常信息显示时间  The duration of show error message                   |
