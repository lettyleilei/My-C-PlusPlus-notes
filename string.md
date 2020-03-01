# string

```
string str1='abcdefg';

int pos = str1.find("de");
int pos = str1.rfind("de");
```
rfind从右往左查找，find从左往右查找

子串substr
```
string email="zhangsan@sina.com";
int pos = email.find("@")
string usrName =email.substr(0,pos);

```