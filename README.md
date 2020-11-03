# 实现：call、aplay、bind

实现call

​    function fn(name, age) {

​      this.name = name;

​      this.age = age;

​    }

​    Function.prototype.call2 = function (obj) {

​      function sy(obj) {

​        let num = Symbol((Math.random()) + (new Date()))

​        if (obj.hasOwnProperty(num)) {

​          return sy(obj)

​        } else {

​          return num

​        }

​      }

​      let ckey = sy(obj);

​      obj[ckey] = this;

​      //使用es6方法

​      //let arr = Array.from(arguments).slice(1)

​      //let res = obj[ckey](...arr)

​      //不使用es6方法

​      let arr = []

​      for (let i = 1; i < arguments.length; i++) {

​        arr[i - 1] = `arguments[${i}]`;

​      }

​      let res = eval('obj[ckey](' + arr.join(',') + ')')

​      delete obj[ckey];

​      return res;

​    }

​    let cThis = {}

​    fn.call2(cThis, '大毛', '黑色');







实现aplay

​     function fn(name, age) {

​       this.name = name;

​       this.age = age;

​     }

​     Function.prototype.aplay2 = function (obj, arr) {

​       // console.log(this === fn)

​       function sy(obj) {

​         let num = Symbol((Math.random()) + (new Date()))

​         if(obj.hasOwnProperty(num)) {

​           return sy(obj)

​         } else {

​           return num

​         }

​       }

​       let ckey = sy(obj);

​       obj[ckey] = this;

​       // 使用es6方法

​       // let res = obj[ckey](...arr);



​       // 不使用es6方法

​       let newArr = []

​       for (let i = 0; i < arr.length; i++) {

​         newArr[i] = `arr[${i}]`;

​       }

​       let res = eval('obj[ckey](' + newArr.join(',') + ')');

​       delete obj[ckey];

​       return res;

​     }

​     let cThis = {}

​     fn.aplay2(cThis, ['大毛1', '黑色1']);