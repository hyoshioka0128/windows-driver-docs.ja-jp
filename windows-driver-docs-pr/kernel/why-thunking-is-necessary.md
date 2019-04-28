---
title: サンキングが必要な理由
description: サンキングが必要な理由
ms.assetid: ea73d355-56e8-4f56-b7e8-4dbddcd19124
keywords:
- サンクの WDK
- WOW64 サンク レイヤー WDK
- 32 ビットの I/O をサポートして WDK 64 ビット、サンキング
- バッファー サイズの WDK カーネル
- DRIVER_DATA 構造体
- ポインターの精度を WDK の 64 ビット
- 固定精度のデータ型を WDK の 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0633f28cd2a8a9e6de09c5040a9e83011d51ecb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374569"
---
# <a name="why-thunking-is-necessary"></a>サンキングが必要な理由





カーネル モード ドライバーでは、ユーザー モード アプリケーションから渡されたすべての I/O バッファーのサイズを検証する必要があります。 32 ビット アプリケーションを渡した場合、64 ビット ドライバーをありませんサンクをポインターの精度のデータ型を含むバッファーが行わ、ドライバーは、実際よりも長くするバッファーを必要とします。 これは、ポインターの精度が Microsoft Windows の 32 ビットと 64 ビット Windows で 64 ビットに 32 ビットであるためです。 たとえば、次の構造体の定義があるとします。

```cpp
typedef struct _DRIVER_DATA
{
    HANDLE           Event;
    UNICODE_STRING   ObjectName;
} DRIVER_DATA;
```

32 ビット Windows でドライバーのサイズに\_データ構造は、12 バイト。

処理**イベント**UNICODE\_文字列**ObjectName** USHORT 長さ USHORT 最大長 PWSTR バッファー 32 ビット (4 バイト) (2 バイト) の 16 ビット 16 ビット (2 バイト) 32 ビット (4 バイト)
 

64 ビット Windows でドライバーのサイズに\_データ構造は、24 バイトです。 (構造体のパディングの 4 バイトが必要なように、**バッファー**メンバーは、8 バイト境界に合わせて調整することができます)。

処理**イベント**UNICODE\_文字列**ObjectName** USHORT 長さ USHORT 最大長空 (構造体埋め込み) PWSTR バッファー 64 ビット (8 バイト) 32 ビット (4 バイト) である 16 ビット (2 バイト) である 16 ビット (2 バイト)64 ビット (8 バイト)
 

64 ビット ドライバーがドライバーの 12 バイトを受け取るかどうか\_データ 24 バイトを想定している場合、サイズの検証は失敗します。 これを防ぐため、ドライバーがドライバーかどうかを検出する必要があります\_32 ビット アプリケーションによって送信されたデータ構造および必要な場合は、サンクが適切に検証を実行する前にします。

たとえば、上記のドライバーの thunked バージョン\_データ構造は次のように定義できます。

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

固定精度のデータ型のみが含まれています、この新しい構造体は、Windows の 32 ビットと 64 ビット Windows で同じサイズです。

ポインター\_32**イベント**UNICODE\_STRING32 **ObjectName** USHORT 長さ USHORT 最大長 ULONG バッファー 32 ビット (4 バイト) (2 バイト) の 16 ビット 16 ビット (2 バイト) 32 ビット (4 バイト)
 

 

 




