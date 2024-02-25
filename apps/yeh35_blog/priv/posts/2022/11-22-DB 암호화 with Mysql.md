%{
title: "DB 암호화 with Mysql fc293c0efc304993a5fe32fbc7124db3.md",
author: "yeh35",
tags: ~w(dev),
description: "",
published: false
}
---
# DB 암호화 with Mysql

게시: No
생성일자: 2022년 11월 22일 오전 9:52
수정일자: 2022년 11월 23일 오후 9:02
태그: Spring, mysql, 암호화

# 배경

일을 하다보면 암호화 안해도 되는 데이터도 많지만 보안에 특히 신경을 써야하는 데이터도 많이 다르게 된다. 예를 들어 이메일, 전화번호, 주소와 같은 개인정보, 카드 번호, 카드 빌키 같은 신용 정보는 무조건 데이터를 암호화 해서 DB에 저장해야한다.

“데이터를 암호화 해야한다”라는 요구사항을 듣는 경우 어떻게 해야할지 고민이 깊어진다.

# 데이터의 종류

먼저 데이터가 어떤 종류의 데이터인지 알 필요가 있다. 어떤 알고리즘을 사용할지 결정하기 위해서도 필요하다.

### **복호화 필요한가?**

가장 먼저 따져봐야하는 것은 “**복호화 필요한가?”**이다. ****

데이터중에는 ‘비밀번호’ 같이 분명히 복호화가 필요 없는 데이터가 존재한다.
단순히 비교만하고 데이터가 극악의 확률로 겹쳐도 된다면 Hash 알고리즘을 사용해서 hash 값으로 저장해도 된다. 

<aside>
💡 Hash 값이라고 원본 데이터가 완벽하게 보호되는 것은 아니다.
기본적으로 Salt 값과 Paper 값을 이용하는 것이 안전하다.

</aside>

### 복호화를 해야하는 경우?

복호화를 해야하는 경우에 고려해야할 사항이 많아진다.
이 이후 이야기는 그와 관련된 내용이다.

# 암호화 방법

## Mysql TDE(Transparent Data Encryption)

<aside>
📌 메모리나 네트워크 전송 단계가 아닌 디스크 저장 단계만 암호화된다.

</aside>

DB단 암호화 방식은 각 Database에서 제공하는 방식을 사용하면 된다.
일단 Mysql 5.7 버전부터 테이블 암호화 기능이 추가되었다.
**Mysql의 암호화는 InnoDB 스토리지 엔진의 I/O 레이어(데이터베이스 서버와 디스크 사이)에서 암호화와 복호화가 진행**됨으로 쿼리를 실행시키고, 처리하는 과정은 암호화한 테이블과 안한 테이블이 동일하게 처리된다.

이러한 암호화 방식을 `TDE(Transparent Data Encryption)` 또는 `Data and Rest Encryption` 이라고 부른다.

## Server Side

주민번호 같이 보안에 중요한 컬럼인 경우 

## Where절로 조회를 해야하는가?

# 저장 방식

# 참고 자료

[Column-Level Encryption in MySQL - Percona Database Performance Blog](https://www.percona.com/blog/column-level-encryption-in-mysql/)