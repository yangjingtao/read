###  理解数据的双向绑定（自己编写）
        <input type="text" id="num1">
        +
        <input type="text" id="num2">
        =
        <input type="text" id="sum">
        
        ·js代码·
            var num1 = document.getElementById("num1");
            var num2 = document.getElementById("num2");
            var sum = document.getElementById("sum");
            num1.oninput = function () {
               var one = parseFloat(this.value) ? parseFloat(this.value) : 0;
               var two = parseFloat(num2.value) ? parseFloat(num2.value) : 0;
               sum.value = one + two;
            };
            num2.oninput = function () {
               var two = parseFloat(this.value) ? parseFloat(this.value) : 0;
               var one = parseFloat(num1.value) ? parseFloat(num1.value) : 0;
               sum.value = one + two;
            };
            
            oninput事件在输入框每一次发生改变都会检测到

###  ng-app     
        指定angular接管的区间
        
###  ng-model      
        模型 -> 数据   只能在input里使用
        
###  ng-init        
        初始化  ng-init="one=0,two=1"
        
###  只要通过指令绑定的数据，他天然就是双向数据绑定

###  ng-controller
       <div ng-controller="ctrl">
             <input type="text" ng-model="aa">
             +
             <input type="text" ng-model="bb">
             =
             <input type="text" ng-model="cc">
         </div>
         
        ####script
        angular.module("myapp",[]).controller("ctrl",function($scope){
                 $scope.aa=0;
                 $scope.bb=1;
                 $scope.cc=$scope.aa*1+$scope.bb*1;
                 $scope.$watch("aa",function(){
                     $scope.cc=$scope.aa*1+$scope.bb*1;
                 });
                 $scope.$watch("bb",function(){
                     $scope.cc=$scope.aa*1+$scope.bb*1;
                 });
             });
        
###  ng-bind        
        <li ng-repeat="z in names">{{z}}</li>//如果网速慢的话页面会显示{{z}}，页面不好看
        <li ng-repeat="z in names" ng-bind="z"></li>//采用ng-bind就会避免
        
###  ng-repeat      
        <li ng-repeat="z in names" ng-bind="z"></li>
        用来迭代数组相当于循环
        
        二维数组循环
        ng-repeat="item in data track by $index"    //第一次循环
        ng-repeat="aa in item track by $index"      //第二次循环

###  $scope.$watch()        
        $scope.$watch("bb",function(){  //监测bb的改变
            $scope.cc=$scope.aa*1+$scope.bb*1;
        });
        
###  ng-show   ng-hide      
        <div class="text-center" ng-show="data.length==0">没有任何商品，赶紧去购物吧</div>
        <table class="table table-bordered" ng-hide="data.length==0">
        
###  filter(过滤)    
        
  1. currency（货币）        {{123456|currency:"$"（货币表示符）:"2"（保留几位小数）}}
        
  2. date（日期）            {{877777777|date:"yyyy-MM-dd hh-mm-ss"}}
        
  3. orderBy(排序)           {{[12,34,5,67,89]|orderBy:"（不传参数就是升序，传入-就是倒序）"}}
        
  4. limitTo(截取)           {{123456|limitTo:4(要截取的位数):2(截取开始的位置)}}
        
  5. 在script中使用filter
         `$filter("orderBy")(data:"en")`  //data时要处理的数据，en是以en来过滤       
        

### ng-transclude(保留被替换的文件中原有的内容)

###  angular----$http
        
        返回一个promise对象