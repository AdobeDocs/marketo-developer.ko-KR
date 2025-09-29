---
title: 스트림 위치
feature: SOAP
description: SOAP에서 시간 시퀀스 데이터의 페이지 매김을 위한 스트림 위치, 간단하고 복잡한 형식, getLeadChanges, getLeadActivity 등에서의 사용에 대해 설명합니다.
exl-id: c3a3fc1e-086b-4822-b2c7-2a7959db557c
source-git-commit: 7557b9957c87f63c2646be13842ea450035792be
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 스트림 위치

스트림 위치 요소는 시간 시퀀싱된 데이터의 하나 이상의 논리 스트림에 대한 위치 참조를 포함한다. 위치 참조는 타임스탬프와 같은 대략적인 외부 사양이거나, 이전 API 호출에 의해 반환된 위치의 불투명한 내부 사양일 수 있다. 스트림 위치들은 복잡한, 다중-요소 타입으로서 정의될 수 있거나, 문자열일 수 있다.

스트림 위치는 데이터를 묶음으로 검색하는 데 사용되며 호출자가 결과를 통해 페이지를 매길 수 있도록 합니다. API 요청 내에서 전달된 스트림 위치는 이전 응답에서 반환된 스트림 위치의 값입니다. 이전 API 호출에서 반환된 스트림 위치는 수정하지 않는 것이 좋으며, 이로 인해 예기치 않은 API 동작이 발생할 수 있습니다.

## 스트림 위치를 지원하는 API

- [getCustomObjects](getcustomobjects.md)
- [getLeadChanges](getleadchanges.md)
- [getLeadActivity](getleadactivity.md)
- [getMObjects](getmobjects.md)
- [getMultipleLead](getmultipleleads.md)

## 단순 스트림 위치

```
<streamPosition>8UJZetaMb1V6uUZl+L7DcPP2jG+PMmtpF</streamPosition>
```

## 복합 스트림 위치

```xml
<startPosition>
  <latestCreatedAt  />
  <oldestCreatedAt>2013-08-01T00:13:13+00:00</oldestCreatedAt>
  <activityCreatedAt  />
  <offset>ID:1086173</offset>
</startPosition>
```
