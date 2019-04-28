---
title: AVStream のフロー制御ゲート
description: AVStream のフロー制御ゲート
ms.assetid: c5592f92-a432-44e3-afe0-60fcf917a443
keywords:
- AVStream 論理ゲート WDK
- gates WDK AVStream のロジック
- ゲート WDK AVStream
- ゲート WDK AVStream
- KSGATE
- フロー制御ゲート WDK AVStream
- gates WDK AVStream のコントロールの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a077e26860ef579a0e39d7b7188f0bd7ed83dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376108"
---
# <a name="flow-control-gates-in-avstream"></a>AVStream のフロー制御ゲート





AVStream は、制御フローのメカニズムとして論理ゲートを使用します。 によって表される各ロジック ゲート、 [ **KSGATE** ](https://msdn.microsoft.com/library/windows/hardware/ff562566)構造体。

AVStream では、各フィルターまたは 1 つとゲートを使用した pin を初期化します。 ミニドライバーは、その特定のオブジェクトがデータを処理する場合を判断するのにこのメカニズムを使用できます。 Pin の処理の制御ゲートを取得するようにミニドライバーを呼び出す[ **KsPinGetAndGate**](https://msdn.microsoft.com/library/windows/hardware/ff563502)します。 フィルター処理コントロール ゲートを取得する[ **KsFilterGetAndGate**](https://msdn.microsoft.com/library/windows/hardware/ff562542)します。

新しいロジックを作成するゲート、ミニドライバー呼び出し[ **KsGateInitializeAnd** ](https://msdn.microsoft.com/library/windows/hardware/ff562574)または[ **KsGateInitializeOr**](https://msdn.microsoft.com/library/windows/hardware/ff562576)します。 状態遷移を転送し、もう 1 つのゲートの入力として、1 つのゲートの出力を使用することができます。 これを行うには、指定、 *NextOrGate*または*NextAndGate*これらの呼び出しのパラメーター。

論理ゲートを既存の入力を閉じるには、呼び出すことができます[ **KsGateTurnInputOff**](https://msdn.microsoft.com/library/windows/hardware/ff562589)します。 ミニドライバーは、この呼び出しを中止し、アクティブな pin を閉じるか、無期限の処理を中断すること。

同様に、呼び出す[ **KsGateTurnInputOn** ](https://msdn.microsoft.com/library/windows/hardware/ff562591)を特定のゲートに既存の入力を開きます。

キャプチャしようとスレッドを処理する準備ができたら、*で*処理するオブジェクトの処理を制御する AND ゲートの入力。 これは、ミニドライバーの呼び出しを行う[ **KsGateCaptureThreshold**](https://msdn.microsoft.com/library/windows/hardware/ff562571)します。

AND ゲートが開いている場合は、AVStream がゲートへの入力をオフにし、処理が開始します。 その他のスレッドをキャプチャできましていない処理中に、ゲートが閉じているようになりましたので、*で*ゲートの入力。 1 つのスレッドは、一度にデータを処理できます。

を変更せず、ゲートの状態を確認するようにミニドライバーを呼び出すことができます[ **KsGateGetStateUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff562572)します。 ただし、この関数が同期を処理しないことに注意してください。

論理ゲートを削除する[ **KsGateTerminateAnd** ](https://msdn.microsoft.com/library/windows/hardware/ff562586)または[ **KsGateTerminateOr**](https://msdn.microsoft.com/library/windows/hardware/ff562588)します。 削除するゲートがゲート チェーンの先頭にあります。

論理ゲートへの入力として、暗証番号 (pin) をアタッチし、フィルターへの入力として同じ論理ゲートを接続し、ゲート、呼び出し[ **KsPinAttachAndGate** ](https://msdn.microsoft.com/library/windows/hardware/ff563491)または[ **KsPinAttachOrGate**](https://msdn.microsoft.com/library/windows/hardware/ff563492).

### <a name="determining-gate-status"></a>ゲートの状態を判断します。

And ゲートの値を**カウント**KSGATE 構造体のメンバーである数を引いた数*オフ*入力。

Count = 1 - (数*オフ*入力)

この値が 0 に等しいまたはそれよりも小さい場合は、ゲートは閉じられます。 この値が 0 より大きい場合は、ゲートが開きます。

値、またはゲートの**カウント**KSGATE のメンバーの数は、*で*ゲートへの入力。

Count = (数*で*入力)

この値が 0 に等しい場合は、ゲートは閉じられます。 場合**カウント**はゼロより大きく、ゲートが開きます。

ゲートが有効な**カウント**の範囲のいずれかまたは。ゲートが有効な**カウント**0 以上の範囲。 設定しない**カウント**に無効な値です。*AVStream では、ミニドライバーが有効な状態にゲートを設定している検証されません。*

 

 




