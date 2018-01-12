---
layout: post
title: "Algorithm: 문자열 뒤집기"
categories:
  - Algorithm

last_modified_at: 2018-01-12
---

스택개념을 이용하면 간단하게 처리할 수 있는 문제다
특정 문자열의 문자들을 스택에 넣고(push) 모든 문자를 스택에 저장하였으면 차례대로 꺼내면 된다(pop)

C와 같이 문자열 자료형이 존재하지 않는 언어에선 스택에 넣고 빼는 과정이 필요하지만, 자바와 같이 문자열 자료형이 존재한다면 그냥 그 문자열을 역으로 하나씩 읽어서 그대로 출력 하면 된다

```java
public class ReverseString {
	
	public String Reverse(String param) {
		
		String result = "";
		
		for(int i=param.length()-1; i>=0; i--) {
			result += param.charAt(i);
		}
		
		return result;
	}
	
	
	public static void main(String[] args) {
		
		ReverseString Reverse = new ReverseString();
		
		System.out.println("Result : "+Reverse.Reverse("apple"));
        //Result : elppa
		
	}
}
```

코드를 보면 ```Reverse ``` 함수에서 문자열 파라미터를 읽어서 루프를 돌면서 역으로 하나씩 읽는다.
그리고 읽어들인 문자를 ```result``` 라는 문자열에 하나씩 넣는다.
