---
title: "DirectXMath 벡터 라이브러리"
categories: 
  - OnlineJudge
last_modified_at: 2019-10-11T13:00:00+09:00
tags: 
  - DirectX
  - C++
toc: true
sidebar_main: true
---

## Intro

> DirectXMath 라이브러리의 벡터

## DirectXMath 라이브러리

`DirectXMath`는 Direct3D 응용프로그램을 위한 표준 3차원 수학 라이브러리이다.

이 라이브러리는 SSE2(Streaming SIMD Extensions 2) 명령 집합을 활용 한다. SIMD 명령들은 128bit 너비의 SIMD(Single Instruction Multiple Data)레지스터들을 이용하여
32bit의 float나 int 네 개를 한번에 처리할 수 있다. 

이는 벡터 연산에서 4차원 벡터 덧셈 명령을 단번에 처리할 수 있게 되어 아주 유용하다.

> SIMD 

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DirectX/vector/simd.png?raw=true)

병렬 프로세서의 한 종류로 하나의 명령어로 여러 개의 값을 동시에 계산한다.[^1]

[^1] : [https://ko.wikipedia.org/wiki/SIMD](https://ko.wikipedia.org/wiki/SIMD)

> DirectXMath 라이브러리 사용

`DirectXMath`라이브러리를 사용하기 위해서는 `DirectXMath.h` 와 `DirectXPackedVector.h` 헤더를 포함시킨다.

## 벡터 형식

`DirectXMath`에서의 벡터 형식은 `SIMD` 하드웨어 레지스터에 대응되는 `XMVECTOR`이다. 128비트 크기이며 32비트 부동소수점 값 네 개로 구성된다.

```c++
typedef __m128 XMVECTOR; 
```

여기서 `__m128` 은 `SIMD` 형식이고 SIMD를 사용하려면 반드시 이 형식이어야 한다. (double은 __m128d, int는 __m128i)

`XMVECTOR`는 16바이트 경계에 정합(Alignment) 되어야하는데, 
여기서 정합은 메모리 상에서 16바이트(128비트) 단위로 묶는것을 의미한다. 

정합은 지역 변수와 전역 변수에서는 자동으로 일어난다. 

클래스나 구조체에서는 `XMVECTOR`대신 `XMFLOAT2, 3, 4`를 사용하는 것이 더 쉽고 간편한 경우가 많기에 권장된다.

> XMFLOAT4 구조체 예시

```c++
struct XMFLOAT4
{
    float x;
    float y;
    float z;
    float w;


 XMFLOAT4() {}
 XMFLOAT4(float _x, float_y, float_z, float _w) :
    x(_x), y(_y), z(_z), w(_w) {}
    
 explicit XMFLOAT4(_In_reads_ (4) const float *pArray) :
    x(pArray[0]), y(pArray[1]), z(pArray[2]), w(pArray[3]) {}
    
 XMFLOAT4& operator = (const XMFLOAT4 Float4)
 {
  x = Float4.x; y = Float4.y; z = Float4.z; w = Float4.w; return *this;
 }
};

```

이 형식을 계산에 직접 사용하면 SIMD의 장점을 얻을 수 없다. 그러므로 인스턴스를 `XMVECTOR` 형식으로 변환해야한다.

`DirectXMath` 라이브러리는 그런 변환을 수행하는 적재(load) 함수와 `XMVECTOR`의 자료를 `XMFLOAT`로 변환하는 저장(store) 함수를 제공한다.

> 요약

1. 지역 변수 전역 변수는 `XMVECTOR`를 사용

2. 클래스, 구조체 멤버는 `XMFLOAT` 사용

3. 계산 수행하기전 적재함수를 이용해 `XMFLOAT`를 `XMVECTOR`로 변환

4. `XMVECTOR`인스턴스로 계산 수행

5. 저장 함수로 `XMVECTOR`를 `XMFLOAT`로 변환

## 적재 및 저장 함수

> 적재 함수

```
XMVECTOR XM_CALLCONV XMLoadFloatn(const XMFLOATn *pSource);
```

`XMFLOATn`을 `XMVECTOR`에 적재


> 저장 함수

```
void XM_CALLCONV XMStoreFloat2(XMFLOATn *pDestination, FXMVECTOR V);
```

`XMVECTOR`를 `XMFLOATn`에 저장

## 매개변수 전달

`XMVECTOR` 인스턴스를 인수로 함수 호출시 효율성을 위해 `stack` 이 아니라 `SSE/SSE2` 레지스터를 통해 함수에 전달되어야 한다. 하지만 인수의 개수는 플랫폼/컴파일러에 따라 다르므로 `FXMVECTOR, GXMVECTOR, HXMVECTOR, CXMVECTOR`라는 형식들을 이용한 호출 규약을 따라야한다. 

이때 호출 규약역시 컴파일러에 따라 다를 수 있어 함수앞에 `XM_CALLCONV`라는 호출 규약 지시자를 붙여야한다.

> XMVECTOR 매개변수 전달에 관한 규칙

1. 처음 세 `XMVECTOR` 매개변수는 `FXMVECTOR` 형식 지정

2. 넷째 `XMVECTOr` 매개변수는 `GXMVECTOR` 지정

3. 다섯째 여섯째는 `HXMVECTOR` 지정

4. 그 이상은 `CXMVECTOR` 지정

5. 이때 매개변수들 사이에 `XMVECTOR`가 아닌 매개변수가 있으면 무시하고 규칙을 적용한다.

6. 생성자에는 처음 세 `XMVECTOR` 매개변수에 `FXMVECTOR`를 이외에는 `CXMVECTOR`를 사용한다. 도한 `XM_CALLCONV` 호출 규약 지시자도 사용하지 않아야한다.

**예시**

```cpp
// 함수에는 XM_CALLCONV를 붙여준다
inline XMMATRIX XM_CALLCONV XMMatrixTransformation(
    FXMVECTOR ScalingOrigin,
    FXMVECTOR ScalingOrientationQuaternion,
    FXMVECTOR Scaling,
    GXMVECTOR RotationOrigin,
    HXMVECTOR RotationQuaternion,
    HXMVECTOR Translation);
```

**`XMVECTOR`가 아닌 매개변수가 있는 경우 예시**

```cpp
inline XMMATRIX XM_CALLCONV XMMatrixTransformation2D(
    FXMVECTOR ScalingOrigin,
    float     ScalingOrientation,
    FXMVECTOR Scaling,
    FXMVECTOR RotationOrigin,
    flaot     Rotation,
    GXMVECTOR Translation);
```

**생성자**

```cpp
XMINLINE XMMATRIX XMMatrixTransformation
	(
		FXMVECTOR ScalingOrigin,
		FXMVECTOR ScalingOrientationQuaternion,
		FXMVECTOR Scaling,
		CXMVECTOR RotationOrigin,
		CXMVECTOR RotationQuaternion,
		CXMVECTOR Translation
	)
```


## 상수 벡터

상수(const) `XMVECTOR` 인스턴스는 `XMVECTORF32` 형식을 사용해야 한다.

초기화 구문을 사용할 때 항상 사용해야한다.

> 예시

```cpp
static const XMVECTORF32 g_vHalfVector = { 0.5f, 0.5f, 0.5f, 0.5f};
```

## 오버로딩 연산자들

`XMVECTOR`의 덧셈, 뺄셈, 스칼라 곱셈등의 여러가지 오버로딩 연산자들

```cpp
XMVECTOR XM_CALLCONV operator+ (FXMVECTOR V);
XMVECTOR XM_CALLCONV operator+ (FXMVECTOR V);

XMVECTOR& XM_CALLCONV operator+= (XMVECTOR& V1, FXMVECTOR V2);
XMVECTOR& XM_CALLCONV operator-= (XMVECTOR& V1, FXMVECTOR V2);
XMVECTOR& XM_CALLCONV operator*= (XMVECTOR& V1, FXMVECTOR V2);
XMVECTOR& XM_CALLCONV operator/= (XMVECTOR& V1, FXMVECTOR V2);

XMVECTOR& operator*= (XMVECTOR& V, float S);
XMVECTOR& operator/= (XMVECTOR& V, float S);

XMVECTOR XM_CALLCONV operator+ (FXMVECTOR V1, FXMVECTOR V2);
XMVECTOR XM_CALLCONV operator- (FXMVECTOR V1, FXMVECTOR V2);
XMVECTOR XM_CALLCONV operator* (FXMVECTOR V1, FXMVECTOR V2);
XMVECTOR XM_CALLCONV operator/ (FXMVECTOR V1, FXMVECTOR V2);
XMVECTOR XM_CALLCONV operator* (FXMVECTOR V, float S);
XMVECTOR XM_CALLCONV operator* (float S, FXMVECTOR V);
XMVECTOR XM_CALLCONV operator/ (FXMVECTOR V, float S);
```

## 기타 상수 및 함수

`DirectXMath`라이브러리는 여러 공식의 근삿값을 구할때 유용한 상수들을 제공한다.

```cpp
const float XM_PI = 3.14592654f;
const float XM_2PI = 6.283185307f;
const float XM_1DVPI = 0.318309886f;
const float XM_1DV2PI = 0.1591543f;
const float XM_PIDIV2 = 1.570796327f;
const float XM_PIDV4 = 0.785398163f;
```

라디안 단위 각도와 도 단위 각도 사이의 변환을 위한 인라인 함수도 제공한다.

```cpp
inline float XMConvertToRadians(float fDegrees) {

return fDegrees * (XM_PI / 180.0f);

}

inline float XMConvertToDegrees(float fRadians) {

return fRadians * (180.0f / XM_PI);

}
```

또한 최소 최댓값 함수도 있다.

```cpp
template<class T> inline T XMMin(T a, T b) { return (a < b) ? a : b; }
template<calss T> inline T XMMax(T a, T b) { return (a < b) ? a : b; }
```


## 설정 함수

`XMVECTOR` 객체 내용을 설정하는 용도로 제공하는 함수들이다.

```cpp
// 0 Vector 반환
XMVECTOR XM_CALLCONV XMVectorZero();

// Vector (1, 1, 1, 1) 반환
XMVECTOR XM_CALLCONV XMVectorSplatOne();

// Vector (x, y, z, w) 반환
XMVECTOR XM_CALLCONV XMVectorSet(float x, float y, float z, float w);

// Vector (s, s, s, s) 반환
XMVECTOR XM_CALLCONV XMVectorReplicate(float Value);

// Vector (vx, vx, vx, vx) 반환
XMVECTOR XM_CALLCONV XMVectorSplatX(FMVECTOR V);

// Vector (vy, vy, vy, vy) 반환
XMVECTOR XM_CALLCONV XMVectorSplatY(FMVECTOR V);

// Vector (vz, vz, vz, vz) 반환
XMVECTOR XM_CALLCONV XMVectorSplatZ(FMVECTOR V);
```

## 벡터 함수들

```cpp
// 벡터의 길이 반환
XMVECTOR XM_CALLCONV XMVector3Length(FXMVECTOR V);

// 벡터의 길이 제곱 반환
XMVECTOR XM_CALLCONV XMVector3LengthSq(FXMVECTOR V);

// V1과 V2의 내적 반환
XMVECTOR XM_CALLCONV XMVector3Dot(FXMVECTOR V1, FXMVECTOR V2);

// V1과 V2의 외적 반환
XMVECTOR XM_CALLCONV XMVector3Cross(FXMVECTOR V1, FXMVECTOR V2);

// V 정규화
XMVECTOR XM_CALLCONV XMVector3Normalize(FXMVECTOR V);

// V에 수직인 벡터 반환
XMVECTOR XM_CALLCONV XmVector30rthgonal(FXMVECTOR V);

// V1과 V2 사이의 각도 반환
XMVECTOR XM_CALLCONV XMVector3AngleBetweenVectors(FXMVECTOR V1, FXMVECTOR V2);

void XM_CALLCONV XMVector3ComponentsFromNormal(
XMVECTOR* pParallel,       // proj_n(v) 반환 
XMVECTOR* pPerpendicular,  // perp_n(v) 반환 
FXMVECTOR V,               // 입력 v
FXMVECTOR Normal);         // 입력 n

// V1 == V2 반환
bool XM_CALLCONV XMVector3Equal(FXMVECTOR V1, FXMVECTOR V2);

// V1 != V2 반환
bool XM_CALLCONV XMVECTOR3NotEqual(FXMVECTOR V1, FXMVECTOR V2);

```

## 부동소수점 오차

컴퓨터에서 벡터를 다룰 때 부동소수점 수들을 비교할 때 부동소수점의 부정확함을 반드시 고려해야한다. 정규화된 벡터의 길이가 정확이 1이 아니므로  거듭제곱 과정에서 오차가 발생할 수 있다. 

> 예시

```cpp
#include <Windows.h> // XMVerifyCPUSupport에 필요함
#include <DirectXMath.h>
#include <DirectXPackedVector.h>
#include <iostream>

using namespace std;
using namespace DirectX;
using namespace DirectX::PackedVector;


int main()
{
	cout.precision(8);

	// SSE2를 지원하는지 확인
	if (!XMVerifyCPUSupport)
	{
		cout << "DirectXMath를 지원하지 않음" << endl;
		return 0;
	}

	XMVECTOR u = XMVectorSet(1.0f, 1.0f, 1.0f, 0.0f);
	XMVECTOR n = XMVector3Normalize(u);

	float LU = XMVectorGetX(XMVector3Length(n));



	// 수학적으로는 길이가 반드시 1이어야 한다
	cout << LU << endl;

	if (LU == 1.0f)
	{
		cout << "길이 1" << endl;
	}
	else
	{
		cout << "길이 1이 아님" << endl;
	}

	// 1을 임의의 지수로 거듭제곱해도 여전히 1이어야 한다
	float powLU = powf(LU, 1.0e6f);
	cout << "LU^(10^6) = " << powLU << endl;

	return 0;

}
```

**실행결과**

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DirectX/vector/float.png?raw=true)

이러한 부정확함 때문에 두 부동소수점의 상등을 판단할 때에는 근사적으로 같은지 판단해야한다. 허용 오차로 사용할 아주작은 수 `Epsilon`을 정하고 `Epsilon`보다 작으면 상등으로 판단한다.

`DirectXMath` 라이브러리는 두 벡터의 상등을 판정하는 `XMVector3NearEqual` 함수를 제공한다. 

```cpp
XMFINLINE bool XM_CALLCONV XMVector3NearEqual(
    FXMVECTOR U,
    FXMVECTOR V,
    FXMVECTOR Epsilon
);
```

## 참고자료

[https://docs.microsoft.com/ko-kr/windows/win32/dxmath/pg-xnamath-getting-started?redirectedfrom=MSDN#type_usage_guidelines_](https://docs.microsoft.com/ko-kr/windows/win32/dxmath/pg-xnamath-getting-started?redirectedfrom=MSDN#type_usage_guidelines_)

[프랭크 D. 루나, DirectX 12를 이용한 3D 게임 프로그래밍 입문, 한빛미디어, 2017, 20쪽](http://www.kyobobook.co.kr/product/detailViewKor.laf?barcode=9788968487798)

[https://m.blog.naver.com/PostView.nhn?blogId=acwboy&logNo=50142788368&proxyReferer=https%3A%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=acwboy&logNo=50142788368&proxyReferer=https%3A%2F%2Fwww.google.com%2F)