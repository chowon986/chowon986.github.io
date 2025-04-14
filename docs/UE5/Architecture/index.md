---
title: 문자열 처리
parent: UE5
nav_order: 1
---

## UE 내부 문자열 표현
- 언리얼 엔진의 모든 문자열은 FString 혹은 TCHAR 정렬 상태로 UTF-16 포맷 메모리에 저장됨<br>
- C++ 소스는 UTF-8 혹은 디폴트 Windows 인코딩 방식을 사용하므로 C++ 소스 코드 안에 문자열을 그대로 사용하는 것을 추천하지 않음

## TCHAR
- 언리얼에서 사용하는 문자 타입
- FString, FName, FText 모두 내부적으로 TCHAR 기반 문자열을 사용

## TEXT
- TEXT()는 리터럴 문자열을 플랫폼에 맞는 형식으로 변환해주는 매크로
- 언리얼에서는 TCHAR[]로 변환됨

## FString
- FName이나 FText와 달리 조작이 가능한 유일한 문자열 클래스
- TCHAR의 TArray로 만들어져 있음
## FName
- 대소문자를 구분하지 않음
- 해시 테이블을 사용하기 때문에 비교 연산 시 id 값만 비교하여 빠름

## FText
- Localization 을 위해 사용
- FString으로 변환 시 데이터 손실이 발생될 수 있음

## 문자열 변환 함수
 - From FName

| From | To | Example |
| -------- | -------- | -------- |
| FName | FString | TestHUDString = TestHUDName.ToString(); |
| FName | FText | TestHUDText = FText::FromName(TestHUDName); |

 - From FString

| From    | To     | Example |
|---------|--------|--------|
| FString | FName  | TestHUDName = FName(\*TestHUDString);   |
| FString | FText  | TestHUDText = FText::FromString(TestHUDString);   |
| FString | int32  | int32 TestInt = FCString::Atoi(\*MyFString);   |
| FString | float  | float TestFloat = FCString::Atof(\*MyFString); |

- From int32/float

| From    | To     | Example |
|---------|--------|--------|
| int32 | FString  | FString TestString = FString::FromInt(MyInt);   |
| float | FString  | FString TestString = FString::SanitizeFloat(MyFloat);  |

 - From FText

| From    | To     | Example |
|---------|--------|--------|
| FText | FString  | TestHUDString = TestHUDText.ToString();  |
| FText | FName  | 직접적인 변환 없음<br> 필요 시 FText->FString->FName 변환 필요 |




참고문서  
- [Unreal Engine 공식 문서](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/string-handling-in-unreal-engine)
