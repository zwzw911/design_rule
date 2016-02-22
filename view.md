#网页设计
### input输入
1. input输入分为两种情况，一种输入后进行判断（例如登录），一种是输入后存储（例如注册）
2. 无论对于那种情况，input都需要在前端和后端进行检测输入数据是否符合标准。  
client端，因为使用angularjs，所以把input分成2部分：用于定义input属性（name，type）；以及定义input检测（require,minLength,maxLength,format,equalTo)。格式是Object而不是Array，angularjs的ng－repeat能够处理Object。      
**Example**:  
userName:{value:'',blur:false,focus:true,inputType:"text",itemIcon:"fa-user",itemLabelName:"用户名",itemExist:false,valid:undefined,errorMsg:""}  
userName:{require:true, minLength:2,maxLength:40, format:regex, equalTo:"another input name"}
  2.1 **是否为空**。    
  通过require属性（bollean）进行判断。    
  client端只要一个错误信息就可以（"不能为空"，然后通过字符串拼接）；    
  server端， 错误信息和client端类似，都是通过字符串拼接；除此之外，还需要额外的rc。   
  2.2 **长度是否符合**    
  client端只要一个错误信息就可以（"不能为空"，然后通过字符串拼接）， name+"最少需要"+minLenght+"个字符"。    
  erver端， 错误信息和client端类似，都是通过字符串拼接；除此之外，还需要额外的rc。  
  2.3 **格式是否符合（mail）**    
  无论client，server端，错误信息需要定制。例如：密码的格式不正确，必须由字符，数字，特殊符号组成。  
  2.4 **等于（再次输入密码）**  
  client使用filter。错误信息单独定义。  
  server使用函数。错误信息单独定义  
3. 需要把检测结果显示  
  如果是正确的，那么input加上success，并且一个勾（可选）。  
  如果检测错误，那么加error，并且一个X（可选）和errorMsg。  
  如果是自动检测（鼠标离开input就开始检测，那么需要blur事件和focus事件，blur进行检测，focus进行复位：去掉class和errorMsg）  
  
### input输出
1. input从数据库读取，需要进行html转义，一边正确显示在网页上，并且防止可能的注入攻击。方法是，注入$sec模块，并且在input上，使用ng-bing-html绑定返回的数据，并用自己建立的filter进行过滤。  
ng-bind-html="article.content | trustHtml"  
myApp.filter('trustHtml', function ($sce) {  
        return function (input) {  
            return $sce.trustAsHtml(input);  
        }  
    });  
