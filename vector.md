# vector容器

```
#include<vector>

void test(){
 vector<int> v;
 
 v.push_back(10);
 v.push_back(20);
 v.push_back(30);
 v.push_back(40);
 
 // 通过迭代器访问容器中的数据
  vector<int>::iterator itBegin=v.begin();
    vector<int>::iterator itEnd=v.end();

 //第一种遍历方式 
 
  //第二种遍历方式 
  for(vector<int>::iterator it=v.begin();it !=v.end(); it++){
  
    cout <<*it<<endl;
}
//第三种遍历方式 ，利用STL提供遍历算法
void myPrint(int val){
    cout<<val<<endl;
}
#include<algorithm>
for_each(v.begin, v.end(),myPrint)

```

```
class Person
{
public:
    Person(string name, int age){
    this->m_name = name;
    this->m_age = age;
    }
    string m_name;
    int m_age;
    
void test(){
    vector<Person> v;
    
    Person p1("aaa",10);
    Person p2("bbb",20);
    Person p3("ccc",30);
    Person p4("ddd",40);
    Person p5("eee",50);
    
    v.push_back(p1);
    v.push_back(p2);
    v.push_back(p3);
    v.push_back(p4);
    v.push_back(p5);
    
    for(vector<Person>::iterator it =v.begin(); it!=v.end(); it++){
        cout<<(*it).m_name<<(*it).m_age<<endl;
    cout<<it->m_name<<it-
    >m_age<<endl;
    }
    
void test02(){
 vector<Person *> v;
    
    Person p1("aaa",10);
    Person p2("bbb",20);
    Person p3("ccc",30);
    Person p4("ddd",40);
    Person p5("eee",50);
    
    v.push_back(&p1);
    v.push_back(&p2);
    v.push_back(&p3);
    v.push_back(&p4);
    v.push_back(&p5);
    
    for(vector<Person*>::iterator it =v.begin(); it!=v.end(); it++){
        
    cout<<(*it)->m_name<<(*it)-
    >m_age<<endl;
    }

}
}
```

vector 容器嵌套容器
```
void test01(){
    vector<vector<int>>
 v;
    vector<int> v1;
    vector<int>v2;
    vector<int>v3;
    vector<int> v4;
    
    for( int i=0;i<4;i++){
        v1.push_back(i+1);
        v2.push_back(i+1);
        v3.push_back(i+1);
        v4.push_back(i+1);
    }
    v.push_back(v1);
    v.push_back(v2);
    v.push_back(v3);
    v.push_back(v4);
    
    for(vector<vector<int>>::iterator it=v.begin(); it!=v.end();it++){
    for(vector<int>::iterator vit=(*it).begin();vit!=(*it).end();vit++){
    cout<<*vit<<endl;
    }
    }
 }
 ```
 
 vector动态扩展，并不是在原空间之后续接新空间，而是寻找更大的内存空间，然后将原数据拷贝新空间，释放原空间
 
 构造
 ```
 vector<int>v1;
 for(int i=0;i<10;i++){
    v1.push_back(i);
 }
 
 vector<int>v2(v1.begin(),v1.end());
 
 //n个elem方式构造，10个100
 vector<int> v3(10,100);
 ```