---
layout: default
title: avalon
---
# avalon code:
```
validatePhone:function(){
            var pass = false;
            if(vm.phone == ''){
                vm.phoneTip = "手机号不能为空";
            }else{
                if(!helper.validate("phone",vm.phone)){
                    vm.phoneTip = "手机号不符合要求";
                }else{
                    vm.phoneTip = "";
                    pass = true;
                }
            }
            return pass;
        },
        validateCode:function(){
            var pass = false;
            if(vm.code == ''){
                vm.codeTip = "验证码不能为空";
            }else{
                if(!helper.validate("sms",vm.code)){
                    vm.codeTip = "验证码不符合要求";
                }else{
                    vm.codeTip = "";
                    pass = true;
                }
            }
            console.log("v code");
            return pass;
        },
        validatePassword:function(){
            var pass = false;
            if(vm.password == ''){
                vm.passwordTip = "密码不能为空";
            }else{
                if(!helper.validate("password",vm.password)){
                    vm.passwordTip = "密码不符合要求";
                }else{
                    vm.passwordTip = "";
                    pass = true;
                }
            }
            return pass;
        },
        validateRepeatPassword:function(){
            var pass = false;
            if(vm.repeatPassword == ''){
                vm.repeatPasswordTip = "密码不能为空";
            }else{
                if(vm.password != vm.repeatPassword){
                    vm.repeatPasswordTip = '两次输入密码不一致';
                }else{
                    vm.repeatPasswordTip = "";
                    pass = true;
                }
            }
            return pass;
        },
        submit:function(){
            var phone = vm.validatePhone();
            var code = vm.validateCode();
            var password = vm.validatePassword();
            var rePass = vm.validateRepeatPassword();
            if(phone && code && password && rePass){
                vm._submit();
            }
        },
```
执行以上代码，每个input都会有提示。
如果是以下代码：
```
        submit:function(){
            var phone = vm.validatePhone(),
                code = vm.validateCode(),
                password = vm.validatePassword(),
                rePass = vm.validateRepeatPassword();
            if(phone && code && password && rePass){
                vm._submit();
            }
        },
```
其结果与以下代码结果一致：
```
        submit:function(){
            if(vm.validatePhone()&&
              vm.validateCode()&&
              vm.validatePassword()&&
              vm.validateRepeatPassword()
            )
        },
```
会发生短路现象，即一旦遇到返回false的情况，代码就不不再往下执行。
但是在纯js中（不使用avalon的情况下）：
```
        submit:function(){
            var phone = vm.validatePhone(),
                code = vm.validateCode(),
                password = vm.validatePassword(),
                rePass = vm.validateRepeatPassword();
            if(phone && code && password && rePass){
                vm._submit();
            }
        },
```
是不会发生短路现象的，每个验证都会执行。
还不知道是为什么，仅仅记录，避免再次掉坑。
