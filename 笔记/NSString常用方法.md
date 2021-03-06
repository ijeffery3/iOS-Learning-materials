
######  2016年来，资本主义的寒冬，互联网创业热潮的散去，伴随着iOS开发行业越来越严峻，前两年只要一两年工作经验的iOS开发者都会受到热捧，而如今，三年工作经验的开发者找工作都举步维艰...
***
######小弟弟我普通二本学校大四学生狗一名，虽然从苹果发布swift语言开始接触iOS开发，如今也有两年时间，但对未来还是很迷茫，但只要技术知识掌握牢固，我相信还是能够在这竞争激烈的社会混一口饭吃，所以利用大四剩余的闲暇时光，总结一下iOS开发的基本知识，巩固自己的同时，希望大家一起学习进步。计划先更新OC的知识笔记，以后会更新Swift一些笔记......
***
##第一弹  NSString常用方法  开始发射

### 字符串初始化

```  
NSString *str = @"我是字符串";  
NSString *str1 = [NSString stringWithFormat:@"我是字符串1"];    
NSString *tempStr = @"我是字符串3";      
NSString *str2 = [NSString stringWithString:tempStr];     
NSLog(@"str=%@ \n str1=%@ \n str2=%@",str,str1,str2);
```
***
### 字符串比较

```  
//1.1 比较两个字符串内容是否相同 //返回布尔值，0表示不相同，1表示相同
BOOL flag = [str isEqualToString:str1];
NSLog(@"flag======%i",flag);
    
//1.2 比较两个字符串你的地址是否相同
BOOL flag1 = (str == str1);
NSLog(@"flag1======%i",flag1);
    
//1.3 比较字符串的大小 compare //NSOrderedAscending  前面的小于后面的; NSOrderedSame,  两个字符串相等;NSOrderedDescending  前面的大于后面的
[str1 compare:str1];
//忽略大小写比较
[str1 caseInsensitiveCompare:str2];
```
***
###  SubString 截取字符串

```     
//从Index位置开始截取字符串，返回该位置后面的字符串   
NSString * sfi = [str1 substringFromIndex:1];   
NSLog(@"sfi = %@",sfi); //是字符串1
   
//截取到Index位置的字符串，返回从0-Index位置的字符串    
NSString *sti = [str1 substringToIndex:2];     
NSLog(@"sti = %@",sti); //我是    

//从某个位置 截取到 某个长度的字符串，      
Range(loc , len)                 
NSRange range = {1, 3};
range.location = 1;    
range.length = 3;
NSString *swr = [str1 substringWithRange:range];
NSLog(@"sti = %@",swr); //是字符
```
***
### Searching 搜索字符串

```

NSString *searchStr = @"我是字符串搜索的方法";
    
// 判断是否以什么开头 hasPrefix
BOOL hp = [searchStr hasPrefix:@"字符串"];
NSLog(@"hp = %i",hp); //0
    
// 判断是否以什么结尾
BOOL hs = [searchStr hasSuffix:@"方法"];
NSLog(@"hs = %i",hs); //1
    
    
//        - (BOOL)containsString:(NSString *)str NS_AVAILABLE(10_10, 8_0);
//字符串中是否包含某个字符串
BOOL cs = [searchStr containsString:@"字符串搜索"];
NSLog(@"cs = %i",cs); //1


//返回搜索的字符串位置和长度
range1 = [searchStr rangeOfString:@"字符串搜索"];
NSLog(@"loc = %lu  len = %lu",range1.location,range1.length); // 2   5
    
range1 = [searchStr rangeOfString:@"字符串搜索" options:NSLiteralSearch];
NSLog(@"loc = %lu  len = %lu",range1.location,range1.length); // 2   5

//在字符串结尾拼接字符串
NSString * sbas = [searchStr stringByAppendingString:@"****"];
NSLog(@"sbas = %@",sbas); //我是字符串搜索的方法****
    
NSString * sbaf = [searchStr stringByAppendingFormat:@"**"];
NSLog(@"sbaf = %@",sbaf); //我是字符串搜索的方法**
```
***
### 字符串大小写转换

```
NSString *changingStr = @"我是changing字符串";
// 将字符串转换为大写
NSString *upStr = [changingStr uppercaseString];
NSLog(@"upStr = %@",upStr); //我是CHANGING字符串
    
// 将字符串转换为小写
NSString *lowStr = [upStr lowercaseString];
NSLog(@"lowStr = %@", lowStr); //我是changing字符串
    
// 将字符串的首字符转换为大写
NSString *caStr = [lowStr capitalizedString];
NSLog(@"caStr = %@", caStr); //caStr = 我是Changing字符串
    
// 字符串与基本数据类型的转换
NSString *strWithNum1 = @"110";
NSString *strWithNum2 = @"100";
    
int value1 = [strWithNum1 intValue];
int value2 = [strWithNum2 intValue];
    
NSLog(@"sum = %i", value1 + value2); //sum =  210
    
// 注意: 如果不是int,double,float,bool,integer,longlong这些类型就不要乱用
NSString *str3 = @"abc";
int value3 = [str3 intValue];
NSLog(@"value3 = %i", value3); // 0
    
// 5.C语言字符串和OC字符串之间的转换
char *cStr = "abcdefg";
NSString *ocStr = [NSString stringWithUTF8String:cStr];
NSLog(@"ocStr = %@", ocStr); //ocStr = abcdefg
    
NSString *newStr = @"abc123";
const char *cStr2 = [newStr UTF8String];
NSLog(@"cStr2 = %s", cStr2); //cStr2 = abc123
```

***
###字符串替换

```
// 需求: 将&符号替换为/
NSString *replaceStr = @"我是用来替换字符串的功能";

// OccurrencesOfString: 要替换谁
// withString: 用谁替换
NSString *sro = [replaceStr stringByReplacingOccurrencesOfString:@"替换" withString:@"已经替换了"];
NSLog(@"sro = %@", sro); //sro = 我是用来 已经替换了 字符串的功能
    
// 1.去除空格  2.将&替换为/
NSString *wstr = @"   http:   &&www.   baidu.com   &img&hahaha.gif   ";
// 去除空格
NSString *kStr = [wstr stringByReplacingOccurrencesOfString:@" " withString:@""];
NSLog(@"kStr = %@", kStr);  //kStr = http:&&www.baidu.com&img&hahaha.gif
// 将&替换为/
NSString *aStr = [kStr stringByReplacingOccurrencesOfString:@"&" withString:@"/"];
NSLog(@"aStr = %@", aStr);  //aStr = http://www.baidu.com/img/hahaha.gif
    
// 替换首尾
NSString *bstr = @"http:&&www.baidu.com&img&hahaha.gif";
NSString *cstr = @"HTTP://www.baidu.com/img/HAHAHA.GIF";
NSCharacterSet *set = [NSCharacterSet whitespaceCharacterSet];
NSString *sbtc = [bstr stringByTrimmingCharactersInSet:set];
NSLog(@"newStr = %@", sbtc); //newStr = http:&&www.baidu.com&img&hahaha.gif
NSCharacterSet *set1 = [NSCharacterSet uppercaseLetterCharacterSet];
NSString *sbtcis = [cstr stringByTrimmingCharactersInSet:set1];
NSLog(@"newStr = %@", sbtcis); //newStr = ://www.baidu.com/img/HAHAHA.
```

***
### 字符串路径相关

```
#pragma mark - 字符串路径相关
NSString *pathStr = @"User/cosyvan/Desktop/oc.txt";
// 判断是否是绝对路径，就是判断字符串是否以/开头
if([pathStr isAbsolutePath])
{
NSLog(@"是绝对路径");
}else{
NSLog(@"不是绝对路径"); //打印
}
    
// 获取文件路径中的最后一个目录，本质就是获取路径中最后一个/后面的内容
NSString *lpc = [pathStr lastPathComponent];
NSLog(@"lpc = %@", lpc); //oc.txt
    
// 删除文件路径中的最后一个目录,就是删除最后一个/后面的内容, 包括/也会被删除
NSString *dlpc = [pathStr stringByDeletingLastPathComponent];
NSLog(@"dlpc  =  %@", dlpc); // User/cosyvan/Desktop
    
// 给文件路径添加一个目录,就是在字符串的末尾加上一个/ 和指定的内容
// 注意: 如果路径后面已经有了/, 那么就不会添加了
//      如果路径后面有多个/, 那么会自动删除多余的/, 只保留一个
NSString *apc = [pathStr stringByAppendingPathComponent:@"haha"];
NSLog(@"apc = %@", apc);  //User/cosyvan/Desktop/oc.txt/haha
    
// 获取路径中文件的扩展名,就是从字符串的末尾开始查找. , 截取第一个.后面的内容
NSString *pe = [pathStr pathExtension];
NSLog(@"pe = %@", pe); // pe = txt
    
// 删除路径中文件的扩展名,就是从字符串的末尾开始查找.,删除第一个.和.后面的内容
NSString *dpe = [pathStr stringByDeletingPathExtension];
NSLog(@"dpe = %@", dpe);  // dpe = User/cosyvan/Desktop/oc
    
// 给文件路径添加一个扩展名,在字符串的末尾加上一个.和指定的内容
NSString *ape = [pathStr stringByAppendingPathExtension:@"jpg"];
NSLog(@"ape = %@", ape);  // ape = User/cosyvan/Desktop/oc.txt.jpg

```
***
### 字符串与文件读写

```
//从文件中读取字符串/Users/xxx/Desktop/js.html
NSString *path = @"/Users/cosyvan/Desktop/js.html";
NSError *error;
NSString *swcof = [NSString stringWithContentsOfFile:path encoding:NSUTF8StringEncoding error:&error];
if (error == nil) {
    NSLog(@"str = %@", swcof);
}else {
    NSLog(@"error = %@", [error localizedDescription]);
}
    
    
//将字符串写入到文件中
NSString *writeStr = @"asdfghjklqewtet";
// atomically 如果传入YES, 字符串写入文件的过程中如果没有写完, 那么不会生成文件
//            如果传入NO, 字符串写入文件的过程中如果没有写完, 会生成文件
NSString *path2 = @"/Users/xxx/Desktop/oc.txt";
BOOL wtf = [writeStr writeToFile:path2 atomically:YES encoding:NSUTF8StringEncoding error:nil];
NSLog(@"wtf = %i", wtf);
```
***
### 分割字符串

```
#pragma mark - 分割字符串

NSString *comStr = @"abdfkasdaaad";
    
NSArray *strArr = [comStr componentsSeparatedByString:@"a"];
for (int i = 0; i < strArr.count; i++) {
NSLog(@"*** = %@",strArr[i]);
}
/***
*2016-10-14 13:57:27.919 NSString练习[4049:125849] *** =
*2016-10-14 13:57:27.919 NSString练习[4049:125849] *** = bdfk
*2016-10-14 13:57:27.920 NSString练习[4049:125849] *** = sd
*2016-10-14 13:57:27.920 NSString练习[4049:125849] *** =
*2016-10-14 13:57:27.920 NSString练习[4049:125849] *** =
*2016-10-14 13:57:27.920 NSString练习[4049:125849] *** = d
 **/
```
***
###可变字符串的常用操作

```
NSMutableString *mutableStr = [NSMutableString stringWithFormat:@"i am a very cool boy"];
    
// 在字符串后面添加字符串
[mutableStr appendString:@"/haha"];
//    [strM appendFormat:@"/age is %i", 10];
NSLog(@"mutableStr = %@", mutableStr);
// 删除字符串中的字符串, 经常利用rangeOfString和deleteCharactersInRange方法配合起来删除指定的字符串
// 1.先查找出指定字符串在字符串中的位置
NSRange rg = [mutableStr rangeOfString:@"cool"];
// 2.删除指定字符串
[mutableStr deleteCharactersInRange:rg];
NSLog(@"mutableStr = %@", mutableStr); //mutableStr = i am a very  boy/haha
    
// 3.在xx前面插入xx字符串
// insertString : 需要插入的字符串
// atIndex: 从哪里开始插入
NSRange rg1 = [mutableStr rangeOfString:@"boy"];
[mutableStr insertString:@"cool" atIndex:rg1.location];
NSLog(@"mutableStr = %@", mutableStr);
```

***
>

新手一个，有哪些写的不对的地方，还请各位程序员哥哥们多多指正，谢谢。MarkDown文档和代码均可在github上下载，地址是
[](https://github.com/CoderVan/iOS-Learning-materials/tree/master/OC%E7%BB%83%E4%B9%A0)