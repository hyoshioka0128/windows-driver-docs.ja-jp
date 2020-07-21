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
ms.openlocfilehash: 70536b398320156eda68efc2c002672052940253
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557741"
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

32ビットの Windows では、ドライバーの \_ データ構造のサイズは12バイトです。 次の表は、DRIVER_DATA 構造体の**イベント**メンバーと**ObjectName**メンバーのサイズを示しています。

|Event|ObjectName (USHORT 長)|ObjectName (USHORT 最大長)|ObjectName (PWSTR Buffer)|
|----|----|----|---|
|32 ビット|16 ビット|16 ビット|32 ビット|
|(4 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|

64ビットの Windows では、ドライバー \_ データ構造のサイズは24バイトです。 (**バッファー**メンバーを8バイトの境界でアラインできるように、構造体の埋め込みの4バイトが必要です)。

|Event|ObjectName (USHORT 長)|ObjectName (USHORT 最大長)|空 (構造体の埋め込み)|ObjectName (PWSTR Buffer)|
|----|----|----|----|----|
|64 ビット|16 ビット|16 ビット|32 ビット|64 ビット|
|(8 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|(8 バイト)|

64ビットドライバーが24バイトのドライバーデータを受け取る場合 \_ 、サイズの検証は失敗します。 これを防ぐには、ドライバーは、ドライバーの \_ データ構造が32ビットアプリケーションによって送信されたかどうかを検出し、検証を実行する前に適切にサンクします。

たとえば、上記のドライバーデータ構造の thunked バージョンは、次のように \_ 定義できます。

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

このテーブルには固定精度のデータ型のみが含まれているので、この新しい構造体は、32ビットの Windows と64ビットの Windows で同じサイズになります。

|Event|ObjectName (USHORT 長)|ObjectName (USHORT 最大長)|ULONG バッファー|
|----|----|----|----|
|32 ビット|16 ビット|16 ビット|32 ビット|
|(4 バイト)|(2 バイト)|(2 バイト)|(4 バイト)|
