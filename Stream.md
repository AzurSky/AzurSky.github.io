# JDK8 Stream
## 概念
Stream是Java8 API心成员，它允许用声明性方式处理数据集合。
## 特点
1. 代码简洁：函数式编程写出的代码简明并且意图明确，使用Stream让你从此告别for循环
2. 多核友好：Java函数式编程使得编写并行程序变得简单，你需要的全部就是调用一下方法。
## 流程
1. 第一步把集合转化为流（Stream）  
list.stream();(常规用)  
list.parallelStream();(并行用)  

2. 第二步操作Strram
## 操作符
两种操作符：中间操作符，终止操作符
### 中间操作符
1. filter  
用于通过设置条件过滤出元素

```JAVA
//取得流中包含a的元素集合
List<String> a = strings.stream().filter(s -> s.contains("a")).collect(Collectors.toList());
```

2. distinct  
返回一个元素各异的流（通过流所产生的hashDode和equals方法实现，就是去重）  
```JAVA
//去除流中重复的元素
List<String> collect = strings.stream().distinct().collect(Collectors.toList());
```

3. limit  
返回一个不超过给定长度的流(分页)，获取流中前n个元素  
```JAVA
//取流中前3个元素
List<String> collect = strings.stream().limit(3).collect(Collectors.toList());
```

4. skip  
返回一个扔掉前n个元素的流,获取流中除去前n个元素的其他所有元素
```JAVA
//取流中除前2以外的全部元素
List<String> collect = strings.stream().skip(2).collect(Collectors.toList());
```

5. map  
接受一个函数作为参数，这个函数会被应用到每个元素上，并将其映射成一个新的元素（使用映射是因为它和转换类似，但是区别在于它是创建一个新版本而不是“修改”），对流中所有元素做统一处理。  
```JAVA
//所有元素全部加一个Hello后缀
strings.stream().map(s->(s.concat("Hello"))).collect(Collectors.toList());
```

6. flatMap  
使用flatMap的效果是，各个数组并不是分别映射成一个流，而是映射成流的内容。所有使用map(Arrays::stream)时生成的单个流都会被合并起来，既扁平化为一个流。  
```JAVA
//所有元素扁平化处理成为一个流
public  void flatmap(){
        List<String> strings = Arrays.asList("abc","","bc","efg","abcd","","jkl");
        List<Character> collect = strings.stream().flatMap(s -> StreamTest.getCharacterByString(s)).collect(Collectors.toList());
    }
public static Stream<Character> getCharacterByString(String str){
        List<Character> characterList = new ArrayList<>();
        for (Character character : str.toCharArray()) {
            characterList.add(character);
        }
        return characterList.stream();
}
```  


7. sorted  
返回排序后的流  

