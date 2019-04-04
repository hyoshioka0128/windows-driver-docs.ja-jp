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
ms.openlocfilehash: c5703850f2a821293a24e90169b10509c48ca4ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571401"
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

デバッグ レベルを設定する 2 つの方法はあります。 まず、スマート カード ドライバーのテスト プログラムを使用して*Scdrvtst*、Windows Driver Kit (WDK) に付属します。 2 つ目は、使用する、 [ **SmartcardSetDebugLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff548960)スマート カード ドライバーのライブラリ ルーチン。

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

リモート デバッグ セッションの設定の詳細については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

 

 





