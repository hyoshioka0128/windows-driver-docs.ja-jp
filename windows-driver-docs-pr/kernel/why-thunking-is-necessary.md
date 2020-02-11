---
title: サンキングが必要な理由
description: サンキングが必要な理由
ms.assetid: ea73d355-56e8-4f56-b7e8-4dbddcd19124
keywords:
- サンク WDK
- WOW64 のサンクレイヤー WDK
- 32ビット i/o サポート WDK 64 ビット、サンキング
- バッファーサイズ WDK カーネル
- DRIVER_DATA 構造体
- ポインターの有効桁数 WDK 64-bit
- 固定精度データ型 WDK 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a2b47ddd1ed4bd94345fa7128cd518e6aa103c
ms.sourcegitcommit: f6aebb32c045b9da7da4bf9b3fd8d6fad05e9deb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2020
ms.locfileid: "77114480"
---
# <a name="why-thunking-is-necessary"></a>サンキングが必要な理由

カーネルモードドライバーは、ユーザーモードアプリケーションから渡された i/o バッファーのサイズを検証する必要があります。 32ビットアプリケーションがポインターの有効桁数のデータ型を含むバッファーを64ビットのドライバーに渡しても、処理が行われない場合、ドライバーはバッファーが実際のサイズより大きいことを期待します。 これは、32ビットの Microsoft Windows ではポインターの有効桁数が32ビット、64ビットの Windows では64ビットであるためです。 たとえば、次の構造の定義について考えてみます。

```cpp
typedef struct _DRIVER_DATA
{
    HANDLE           Event;
    UNICODE_STRING   ObjectName;
} DRIVER_DATA;
```

32ビットの Windows では、ドライバー\_データ構造のサイズは12バイトです。

|イベントの処理|UNICODE\_文字列 ObjectName|||
|----|----|----|---|
||**USHORT 長**|**USHORT の最大長**|**PWSTR バッファー**|
|32ビット|16ビット|16ビット|32ビット|
|(4 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|

64ビットの Windows では、ドライバー\_データ構造のサイズは24バイトです。 (**バッファー**メンバーを8バイトの境界でアラインできるように、構造体の埋め込みの4バイトが必要です)。

|イベントの処理|UNICODE\_文字列 ObjectName||||
|----|----|----|----|----|
||**USHORT 長**|**USHORT の最大長**|**空 (構造体の埋め込み)**|**PWSTR バッファー**|
|64ビット|16ビット|16ビット|32ビット|64ビット|
|(8 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|(8 バイト)|

64ビットドライバーが24バイトのドライバー\_データを受信した場合、サイズの検証は失敗します。 これを防ぐには、ドライバー\_データ構造が32ビットアプリケーションによって送信されたかどうかを検出し、検証を実行する前に、ドライバーが適切にサンクを行う必要があります。

たとえば、上記のドライバー\_の thunked バージョンは、次のように定義できます。

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

このテーブルには固定精度のデータ型のみが含まれているので、この新しい構造体は、32ビットの Windows と64ビットの Windows で同じサイズになります。

|ポインター\_32 イベント|UNICODE\_STRING32 ObjectName|||
|----|----|----|----|
||**USHORT 長**|**USHORT の最大長**|**ULONG バッファー**|
|32ビット|16ビット|16ビット|32ビット|
|(4 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|
