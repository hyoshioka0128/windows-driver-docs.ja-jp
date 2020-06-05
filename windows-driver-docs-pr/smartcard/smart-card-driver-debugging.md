---
title: スマート カード ドライバーのデバッグ
description: スマート カード ドライバーのデバッグ
ms.assetid: 701528f6-d8ba-4a73-ad68-cb35497a3474
keywords:
- スマートカードドライバー WDK、デバッグ
- ドライバーのデバッグ WDK スマートカード
- DebugLevel
- ベンダー提供のドライバー WDK スマートカード、デバッグ
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5512a2a8bb632abe73d3763dc75634a7a083834c
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428325"
---
# <a name="smart-card-driver-debugging"></a>スマート カード ドライバーのデバッグ

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

スマートカードのドライバーライブラリでは、いくつかのデバッグ機能がサポートされています。 各デバッグ機能は、 *Smclib*ヘッダーファイルで定義されている次の定数のいずれかによって表されます。

```cpp
DEBUG_IOCTL
DEBUG_ATR
DEBUG_PROTOCOL
DEBUG_DRIVER
DEBUG_TRACE
DEBUG_ERROR
DEBUG_BREAK
DEBUG_ALL
```

有効なデバッグ機能の組み合わせセットは、*デバッグレベル*と呼ばれる値によって表されます。 この値を計算するには、有効にする機能に対応する定数のビットごとの OR を使用します。

デバッグレベルを設定するには、2つの方法があります。 まず、Windows Driver Kit (WDK) に付属しているスマートカードドライバーのテストプログラム*Scdrvtst*を使用できます。 2つ目は、 [**Smartcardsetdebuglevel**](https://docs.microsoft.com/previous-versions/ff548960(v=vs.85))スマートカードドライバーライブラリルーチンを使用することです。

どちらの場合も、デバッグレベルを設定するプログラムまたはルーチンに、必要なデバッグレベルの値を渡す必要があります。 たとえば、スマートカードライブラリルーチンを使用してドライバーからデバッグレベルを設定するには、次の呼び出しを行います。

```cpp
SmartcardSetDebugLevel(DebugLevel);
```

リーダードライバーからデバッグメッセージを書き込むには、ドライバーが次のルーチンを呼び出す必要があります。

```cpp
SmartcardDebug(
 ULONG DebugLevel,
 PCHAR Message
);
```

> [!IMPORTANT]
> デバッグメッセージを取得するには、オペレーティングシステムのチェックされたバージョンとドライバーのチェックされたバージョンをインストールする必要があります。

このルーチンは、次の方法でリモートデバッガーにメッセージを書き込むために使用することもできます。

- エラーメッセージを書き込むには、 \_ *DEBUGLEVEL*の DEBUG error 定数を使用します。

- 標準のドライバーメッセージを書き込むには、DEBUG driver 定数を使用し \_ ます。

- リーダードライバーがルーチンを開始または終了したことを示すトレースメッセージを作成するには、デバッグ \_ トレースを*debuglevel*として使用します。

ドライバーの開発中に、チェックされたバージョンのスマートカードドライバーライブラリを使用し、Driverentry ルーチンで**Smartcardsetdebuglevel**(DEBUG ALL) を使用してデバッグレベルを最大に設定し \_ ます。 *DriverEntry*

リモートデバッグセッションの設定の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。
