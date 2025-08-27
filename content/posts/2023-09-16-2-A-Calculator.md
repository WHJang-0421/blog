---
title:  "인터프리터 2: A Calculator"
author: "Woohyuk Jang"
draft: false

date: "2023-09-16"
description: ""
categories:
  - cs/compilers
tags:
  - Blog
---
### 인터프리터 #2: A Calculator



이 블로그 포스트는 [Crafting Interpreters](https://craftinginterpreters.com/)를 읽은 후 정리한 글이다. 구현은 [여기](https://github.com/WHJang-0421/make-interpreters)에 했으며 책의 코드를 그대로 따라했다.



우선 lox language에서 가장 간단한 사칙연산, 숫자, 문자열, 괄호 등만 구현한면 calculator가 된다.



1. 주의사항



* 실제로 쓸모 있는 프로그래밍 언어가 되려면 오류를 잘 처리해야 한다. 이는 Scanner, Parser, Interpreter를 만들 때 항상 염두에 두어야 한다.



2\. Scanner



* Scanner는 코드를 받아서 토큰들로 나누는 작업을 담당한다.

* lexeme: 토큰을 나타내는 문자열이다. 코드에서 가장 의미 있는 최소의 단위라고 생각해도 된다. 예를 들면 `print(a)`에서 `print` `(` `a` `)` 가 lexeme이다.

* lexeme을 알면 token을 만들 수 있다. token은 lexeme 값 말고도 코드 상 위치, 토큰 타입 등의 유용한 정보를 포함한다.

* 대부분의 언어 (python, haskell을 제외)는 regular language이다. regular language가 뭔지는 [Chomsky hiearchy](https://en.wikipedia.org/wiki/Chomsky_hierarchy)를 참고하자. (나도 모른다. 이 책은 실습에 집중하는 책이어서 이론은 자세히 설명 안 한다)

* maximal munch: 스캐닝 과정에서 여러개의 규칙이 적용될 수 있는 경우, 가장 많은 문자와 매칭되는 규칙을 채택한다.



3\. BNF와 AST



* 코드에서 토큰 만드는 것과 달리 토큰에서 트리 만드는 것은 임의의 깊이를 지원할 수 없다. 그래서 Context-free grammar를 사용해야 한다.

* BNF (Backus-Naur form)과 그 변종들을 이용하여 프로그래밍 언어를 정의한다. 저자는 책에서 약간의 변형을 준 BNF를 사용했다.



```

expression     → equality ;

equality       → comparison ( ( "!=" | "==" ) comparison )* ;

comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;

term           → factor ( ( "-" | "+" ) factor )* ;

factor         → unary ( ( "/" | "*" ) unary )* ;

unary          → ( "!" | "-" ) unary

               | primary ;

primary        → NUMBER | STRING | "true" | "false" | "nil"

               | "(" expression ")" ;

```



* `"==”` 같은건 terminal이다. 반면에 `expression` 은 non-terminal로, 다른 규칙을 가리킨다.

* precedence: `equality`의 body에 `comparison`이 자리잡고 있기 때문에, `equality`보다 `comparison`의 우선순위가 높다.

* associativity: `term`을 보면 `+, -`는 left-associative임을 알 수 있다.



AST (abstract syntax tree)를 위한 노드도 정의하는데, 코드가 반복적이라서 metaprogramming을 이용했다.



4\. Parser



* Visitor Pattern을 이용하여 AST를 구현했다.

* 파서를 만드는 여러 방법 중 Recursive Descent Parsing을 이용했다.

* Java의 Exceptions를 이용하여 오류가 난 경우 statement level까지 올라와서 다시 파싱을 시작하도록 한다. 지금 단계에서 이는 그냥 맨 위 레벨까지 올라온다는 뜻이다.



5\. Interpreter



* AST의 노드를 방문하여 evaluate하면 된다. 꽤 뻔하다.



By [Woohyuk Jang](https://medium.com/@morrranii) on [September 16, 2023](https://medium.com/p/9d729ffc665d).

Exported from [Medium](https://medium.com) on August 26, 2025.
