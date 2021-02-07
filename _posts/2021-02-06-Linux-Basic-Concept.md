---
title: "Linux의 기본 개념"
categories: 
  - Linux
tags:
  - linux
  - basic
  - concept
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}

> Unix와 Linux에 기본 개념에 대해서 알아보도록 합니다.

## 1. 기본 개념

### 1. 작동방식

참조 글 : [쉘이란?](https://devkingdom.tistory.com/185), [커널이란?](https://www.redhat.com/ko/topics/linux/what-is-the-linux-kernel), [시스템 콜(시스템 호출이란?)](https://luckyyowu.tistory.com/133), [Unix란 무엇인가?](https://namu.wiki/w/UNIX?from=%EC%9C%A0%EB%8B%89%EC%8A%A4)

- 사용자는 **쉘**이라는 프로그램과 대화를 합니다.(입력이 바로 Unix와 대화를 의미하지 않습니다.)
- 쉘은 사용자로부터 Unix를 보호하고, Unix 또한 사용자를 보호합니다.
- Unix의 모든 일은 **커널**이라는 친구가 처리합니다.
- 프로그램들만이 **시스템 콜**을 통해 커널과 대화합니다.
- 쉘은 사용자 입력한 명령어를 해석 또는 실행시키고 다른 프로그램에게 넘겨주는 역할을 수행합니다.