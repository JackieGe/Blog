Typescript完全严格地兼容js吗？
Typescript官方说它是Javascript的超集，好多人也是这么理解的。 本人验证过一些case，得出结论：并不是严格的超集。

例一：

contact.js

function contact() {
    this.name = "Jackie Ge"

    return {
        cname: this.name,
        getCname() {
            return this.cname
        }
    }
}

var c = new contact
console.log(c.cname, c.getCname())
如果是contact.ts， 那么tsc编译的时候出错：error TS2350: Only a void function can be called with the 'new' keyword.

例二：

function Foo() {

}

Foo.array = [1, 2, 3]
Foo.min = function () {
    return Math.min(...this.array)
}

var obj = {
    array: [3, 6, 9]
}
console.log(Foo.min())
console.log(Foo.min.apply(obj))
tsc的时候报错：
error TS2339: Property 'array' does not exist on type '() => void'.
error TS2339: Property 'min' does not exist on type '() => void'

我想说的是，最好总是要做一些实地测试， 不要人云亦云。而且微软的东西做广告的成分较大，最好抱着怀疑的态度。微软技术从COM， VB， JScript， 到WPF， SilverLight，坑害了一代又一代的程序员，真是毁人不倦。目前Typescript又有这个架势。所以玩笑的说，程序员珍爱生命，远离微软。

Typescript优缺点分析
主观的分析TypeScript有其自身的优点：

若类型的静态类型检查。 但这多半是给后端java／C#开发写前端降低门槛， 使之短时间内写出了所谓的前端代码。
ts是为了让新手也能写出不至于太寒碜的代码，便于团队的合作。
但缺点也明显：

有些第三方的js库缺失dts，或者dts更新不及时。会导致不能便利的使用它或者调用了过时的方法／函数
但如果已是熟练的前端开发， TypeScript有时候确实是桎梏。它强制你写一堆繁琐的接口类型。而且有些js的方式它还不兼容 （看我的上面的例子）
它其实阉割了js的一些技法，（还是看我的例子）。要想修炼高手，须要远离ts。所谓可远观而不可近
