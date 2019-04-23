---
title: バグ チェック 0 xea THREAD_STUCK_IN_DEVICE_DRIVER
description: THREAD_STUCK_IN_DEVICE_DRIVER のバグ チェックでは、0x000000EA の値を持ちます。 これは、デバイス ドライバーのスレッドが際限なく回転していることを示します。
ms.assetid: f3d6acaf-3445-4fc3-b4ed-b72a74a32b57
keywords:
- バグ チェック 0 xea THREAD_STUCK_IN_DEVICE_DRIVER
- THREAD_STUCK_IN_DEVICE_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THREAD_STUCK_IN_DEVICE_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 402c9d102e9f80e0ed4165d4711d4ebd38d9fe83
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903034"
---
# <a name="bug-check-0xea-threadstuckindevicedriver"></a>バグ チェック 0xEA:スレッド\_STUCK\_IN\_デバイス\_ドライバー


スレッド\_STUCK\_IN\_デバイス\_ドライバーのバグ チェックが 0x000000EA の値を持ちます。 これは、デバイス ドライバーのスレッドが際限なく回転していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="threadstuckindevicedriver-parameters"></a>スレッド\_STUCK\_IN\_デバイス\_ドライバーのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>スレッドのスタック オブジェクトへのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>DEFERRED_WATCHDOG オブジェクトへのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>問題のあるドライバー名へのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><strong>カーネル デバッガー。</strong>「傍受」バグ チェック 0 xea 回数がヒットしました</p>
<p><strong>青い画面。</strong>1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ほとんどの場合、アイドル状態になるハードウェアを待って、無限ループには、デバイス ドライバーが回転しています。

これは通常、ハードウェア自体、またはハードウェアのプログラミング、デバイス ドライバに問題を示します。 多くの場合、これは、不適切なビデオ カード、または不適切なディスプレイ ドライバーの結果です。

<a name="resolution"></a>解決方法
----------

使用して、 [ **.thread (登録コンテキストの設定)** ](-thread--set-register-context-.md)パラメーター 1 と共にコマンド。 使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)スレッドがスタックしている場所を見つけます。

接続されていると、実行中、カーネル デバッガーが既にある場合と Windows は、タイムアウト条件を検出します。 **DbgBreakPoint**の代わりに呼び出される**KeBugCheckEx**します。 詳細なメッセージは、デバッガーに印刷されます。 参照してください[、Debugge に出力を送信する](sending-output-to-the-debugger.md)詳細についてはします。

このメッセージとなっていたバグ チェック パラメーターが含まれます。 実際のバグ チェックは実行されませんでした、ため、 [ **.bugcheck (表示バグ データを確認する)** ](-bugcheck--display-bug-check-data-.md)コマンドを利用できません。 使用して 4 つのパラメーターがウォッチドッグのグローバル変数から取得することもできます**dd ウォッチドッグ! g\_WdBugCheckData L5**"32 ビット システム上または**dq ウォッチドッグ! g\_WdBugCheckData L5**"で、64 ビット システム。

これにより、問題が発生したスレッドを検索するなど、対話型の方法でこのエラーのデバッグで、ブレークポイントを設定しを使用して[ **g (移動)** ](g--go-.md)をさらにデバッグ スピン コードに戻ります。

(OS ビルド 3790 またはそれ以前) マルチプロセッサ コンピューターで、スピン中のスレッドがハードウェア割り込みによって中断され、バグのチェック時に、ISR または DPC ルーチンが実行されている場合、タイムアウトをヒットすることができます。 タイムアウトの作業項目を配信し、2 つ目の CPU と同じ時間で処理されるためです。 このような場合、タイムアウトが発生する原因となった、回転のコードを確認、問題のあるスレッドのスタックを詳しく見て必要があります。 使用して、 [ **dds (表示語およびシンボル)** ](dds--dps--dqs--display-words-and-symbols-.md)これを行うコマンド。

 

 




