# c++对象模型和this指针

成员变量和成员函数分开存储
-------
在c++中，类内的成员变量和成员函数分开存储
只有非静态成员变量才属于类的对象

```
class Person 
{
   
}

class PersonA 
{
    int m_A;//非静态成员变量，属于类的对象上，只有这一类占类的对象内存空间
}

void test01(){
    Person p;//空对象占用内存空间为 1，c++编译器会给每个空对象也分配一个字节空间，为了区分空对象占内存的位置。每个空对象也应该有一个独一无二的内存地址
    PersonA pa;占用空间为4
}
```

this指针
-------

每一个非静态成员函数只会但是一份函数实例，也就是说多个同类型对象会共用一块代码。问题：这一块代码是如何区分哪个对象调用自己的呢？

c++通过提供特殊的对象指针，this指针，解决上述问题，this指针指向被调用的函数所属的对象。

this指针的用途：
* 解决名称冲突：当形参和成员变量同名时，可用this指针来区分。

```
class Person{
public:
    Person(int age){
    //this指针指向的是被调用的成员函数所属的对象，相当于python中的self
        this->age=age;
    }
    int age;
    void PersonAddAge(Person &p){
        this->age+=p.age;
    }
    Person& PersonAddAge02(Person &p){
        this->age+=p.age;
        return *this;
    }
}
```
* 在返回对象本身：类的非静态成员函数中返回对象本身，可使用return *this

```
void test01(){
    Person p1(10);
    Person p2(10);
    p2.PersonAddAge(p1);//链式编程
    p2.PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1);
}
```

空指针访问成员函数
-------
c++中空指针也是可以调用成员函数的，但是也要注意有没有用到this指针
如果用到this指针，需要加以判断保证代码的健壮性

```
class Person{
public:
    void showClassName(){}
    void showName(){
        
        cout<<m_age;
    }
     void showName02(){
        if(this==NULL){
            return;
        } 
        cout<<m_age;
    }
    int m_age;
}
void test01(){
    Person *p=NULL;
    p->showClassName();//没问题
    p->showName()；//报错，会访问到m_age，NULL根本没有
}
```

const修饰成员函数
-------


常函数
* 成员函数加const后我们称这个函数为常函数
* 常函数内不可以修改成员属性
* 成员属性声明时加关键字mutable后，在常函数中依然可以修改

常对象
* 声明对象前加const称改对象为常对象
* 常对象只能调用常函数

```
class Person{
public:
    //this指针的本质 是指针常量，指针的指向是不可以修改的，但是this指针指向的值是可以修改的 Person *const this;
    void showPerson(){
        m_A=100;
    }
    int m_A;
    mutable int m_B;//特殊变量，即使在常函数中，也可以修改这个值
    //加const之后 就相当于 const Person *const this;不仅this指向不能修改，this指向的值也不可以修改
    void showPerson02() const{
        m_A=100;//错误
    }

    
}
```
```
vois test02(){
    const Person p;//在对象前加const，变为常对象
    p.m_A=100;//错误
    p.m_B = 100//正确；
    //常对象只能调用常函数
    p.showPerson02();//正确
     p.showPerson();//错误
    
}
```