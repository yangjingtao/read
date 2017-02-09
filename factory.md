## 服务  config(优先执行)

    ·1·
    angular.module("myapp",[]).config("$ABC",function(){
            return function(){
                console.log(1);
            }
      })
    
    ·2·  
    angular.module("myapp",[]).config("$ABC",function(){
                   return function(){
                       console.log(1);
                   }
             })
                
                
## 指令 directive     

    ·1·
    .directive("abc",function(){
            return {
                restrict:"ECMA", //E(element元素的方式解析)，A(attr属性的方式解析)，M(注释方式解析)
                template:"<div>div</div>"  //传入一个字符串
            }
    })
    
    ·2·  
    .directive("abc",function(){
               return {
                   restrict:"A", //E(element元素的方式出现)，A(attr属性的方式出现)
                   templateUrl:"demo.html", //引入一个文件替换掉abc
                   replace:true，//demo.html中只有一个根标签
                   transclude:true,  //保留原文件中的内容
                   scope:true||false||=||"@"||"&"||{}
                   link:function(a,b,c){
                       //指令自己携带数据 a相当于$scope
                       a.abc="123"
                   }
               }
    })   
    
 
###  ajax在地址栏里留不下任何信息

   1. 搜索引擎不友好
   
   2. file（），http，https，ftp，svn