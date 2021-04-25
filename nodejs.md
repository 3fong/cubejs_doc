let,const,var,window:
    var用于声明变量,可以用于任何范围内;
    let用于声明局部变量,只在代码块中有效;
    const:用于声明常量,基本数据类型值不可变,引用数据类型指针不变.类似于final;
    顶层对象:js运行的宿主环境变量,window对象和global对象.es5全局变量和顶层对象的赋值等同;ES6规定var命令和function命令声明的全局变量，依旧是顶层对象的属性;但let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。