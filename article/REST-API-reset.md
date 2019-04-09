## 描述
在使用我们的Portal REST API过程中，官方Portal REST API文档是有缺失的，即有些API并没有在官方文档里说明，我们只能通过抓取某一操作过程的后台请求来确定具体使用了哪个API，所以这给我们的开发工作带来了很大的不便，此系列文章逐渐将这些官方没有说明的API进行补充说明。   
今天就介绍Portal中用来进行用户密码重置的接口——reset接口。

## 接口参考地址
`https://主机域名/arcgis/sharing/rest/community/users/用户名/reset`

## 接口使用方法
此接口根据传递参数的不同，可以有两种使用方法，下面具体介绍这两种调用方法：   
1. 知道原密码、新密码的情况   
在知道原密码、新密码的情况下，我们向此接口传递的参数分别是：**旧密码、新密码、确认后的新密码、token**这四个参数。如果密码重置成功，会返回用户名和修改的状态（一般是true），下面来看具体的接口调用：   
```
	//token生成成功，重置密码
	$.ajax({
		url:"https://ynxqwportal.arcgis.cn/arcgis/sharing/rest/"+
	 +"community/users/"+$("#username").val()+"/reset",
		type:"POST",
		data:{
			password: $("#oldpassword").val(),       //旧密码
			newPassword: $("#newpassword").val(),    //新密码
			newPassword2: $("#newpassword").val(),   //新密码
			oauth_state: portalToken,                //生成的token
			f:"json"
		},
		dataType:"json",
		async:false,
		success:function(data02){
			console.log(data02);
			if(data02.success){
				alert("密码修改成功");
			}else{
				alert("密码修改失败");
			}
		},
		error:function(e02){
			console.log(e01);
		}
	});
```   

执行成功后我们可以在浏览器的控制面板看到具体的请求、返回信息，如下：