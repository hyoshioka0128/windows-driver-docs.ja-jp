---
title: スマート カード ドライバーのデバッグ
description: スマート カード ドライバーのデバッグ
ms.assetid: 701528f6-d8ba-4a73-ad68-cb35497a3474
keywords:
- スマート カードのドライバー WDK、デバッグ
- ドライバー WDK のスマート カードのデバッグ
- DebugLevel
- ベンダーから提供されたドライバー WDK のスマート カードのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b7b6fe3323aa5e44c57bfc9a0f192935837612d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356672"
---
# <a name="smart-card-driver-debugging"></a>スマート カード ドライバーのデバッグ


## <span id="_ntovr_smart_card_driver_debugging"></span><span id="_NTOVR_SMART_CARD_DRIVER_DEBUGGING"></span>


スマート カードのドライバー ライブラリでは、いくつかのデバッグ機能をサポートします。 定義されている次の定数のいずれかで表される各デバッグ機能、 *Smclib.h*ヘッダー ファイル。

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

有効なデバッグ機能を組み合わせたセットと呼ばれる値で表される、*デバッグ レベル*します。 この値を計算するには、有効に機能に対応する定数のビットごとの OR を取得します。

デバッグ レベルを設定する 2 つの方法はあります。 まず、スマート カード ドライバーのテスト プログラムを使用して*Scdrvtst*、Windows Driver Kit (WDK) に付属します。 2 つ目は、使用する、 [ **SmartcardSetDebugLevel** ](https://docs.microsoft.com/previous-versions/ff548960(v=vs.85))スマート カード ドライバーのライブラリ ルーチン。

どちらの場合も、プログラムまたはルーチンのデバッグ レベルを設定するとするデバッグ レベルの値を渡す必要があります。 たとえば、スマート カードのライブラリ ルーチンを使用して、ドライバーから デバッグのレベルを設定するには、次の呼び出しを行います。

```cpp
SmartcardSetDebugLevel(DebugLevel);
```

**重要な**  オペレーティング システムのチェック済みバージョンとデバッグ メッセージを取得するドライバーのチェック済みバージョンをインストールする必要があります。

 

リーダーのドライバーをドライバー デバッグ メッセージを書き込むには、次のルーチンを呼び出す必要があります。

```cpp
SmartcardDebug(
 ULONG DebugLevel,
 PCHAR Message
);
```

このルーチンがリモート デバッガーに、次の方法でメッセージを書き込むこともできます。

-   エラー メッセージを書き込むには、デバッグを使用して\_のエラーの定数、 *DebugLevel*します。

-   標準のドライバーのメッセージを書き込む、デバッグを使用して、\_ドライバーの定数。

-   リーダーのドライバーが入力またはルーチンの終了を示すトレース メッセージを書き込むには、デバッグを使用して\_としてトレース、 *DebugLevel*します。

ドライバーの開発中に、スマート カードのドライバー ライブラリのチェック済みバージョンを使用し、デバッグ レベルを使用して、最大値に設定**SmartcardSetDebugLevel**(デバッグ\_すべて) で、 *DriverEntry*ルーチン。

リモート デバッグ セッションの設定の詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。

 

 





