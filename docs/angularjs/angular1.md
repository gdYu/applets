 
 + angular-file-upload  
 
 + $q
 
 + **ngModel.$validators**  
 
    validate出现在了当每一次值修改的时候。   
    比如：ngModel.$validators.validateType = function validate(){'执行语句/返回状态'}    
    这样每当ngModel的值改变的时候，就会自动调用。   
    ```
    实例： 
    ngModule.directive('validateTypeDirective',function(){
        return {
            require:'ngModel',
            link:function(scope,ele,attrs,ngModel){
                ngModel.$validators.validateType = function(value){
                    // 执行判断
                    return true/false                
                }
            }
        }
    })
    <form name="myForm">
        <div>
            <input type="text" name="type" ng-model="type" validate-type required/>
            <div ng-if="myForm.type.$error.required">
                you did not enter a type
            </div>
            <div ng-if="myForm.type.$error.validateType">
                some tips
            </div>
        </div>
    </form>
    ```
    
 + ngModel.$render
    ```
    var origRender = ngModel.$render;
    ngModel.$render = render;
    function render(){
        origRender(); // ngModel.$render已被修改，此处调用初始值，触发原本应有逻辑
    }
    ```