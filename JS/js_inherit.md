#JS实现继承

##1.原型链实现继承
####原型链实现继承实际是，利用原型让一个引用类型继承另一个引用类型的属性和方法

例：

	function SuperType () {
	    this.property = true;
	    this.arr = [1];
	}
	SuperType.prototype.getSuperValue = function () {
	    return this.property;
	}
	function SubType () {
	    this.subProperty = false;
	}
	//继承SuperType
	SubType.prototype = new SuperType();
	console.log(SubType.prototype.__proto__ === SuperType.prototype); //true
	SubType.prototype.getSubValue = function () {
	    return this.subProperty;
	}
	let instance = new SubType();
	/*
	*上面将SubType的prototype重写，通过__proto__属性指向了SuperType.prototype,
	从而使得instance的constructor指向SuperType而不是SubType.(constructor属性也是从原型继承而来，原型的constructor指向SuperType)
	*/
	console.log(instance.getSubValue());//false
	console.log(instance.getSuperValue());//true


例子中的实例以及构造函数和原型之间的关系如图：
![](https://i.imgur.com/C9OWER0.png)

在实际的原型链中，所有得引用类型都是继承得Object,所以上图中还少了一段原型链。

完整的原型链：

![](https://i.imgur.com/4s5iCN1.png)

####确定原型和实例的关系
instanceof操作符和isPrototypeOf()方法

例：

	instance instanceof Object//true
	instance instanceof SuperType//true
	instance instanceof SubType//true

	Object.prototype.isPrototypeOf(instance)//true
	SuperType.prototype.isPrototypeOf(instance)//true
	SubType.prototype.isPrototypeOf(instance)//true


