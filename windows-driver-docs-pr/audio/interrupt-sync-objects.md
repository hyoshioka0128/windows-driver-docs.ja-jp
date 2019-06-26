---
title: 割り込み同期のオブジェクト
description: 割り込み同期のオブジェクト
ms.assetid: c9e228e0-6178-442d-a82a-6b14ed67c9d2
keywords:
- ヘルパー オブジェクトの WDK オーディオ、割り込み同期オブジェクト
- 同期オブジェクトの WDK オーディオを中断します。
- IInterruptSync インターフェイス
- 同期の WDK オーディオ
- 割り込みサービス ルーチン WDK オーディオ
- Isr WDK オーディオ
- 非割り込みルーチン WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a98c5cfb3c3da30d781916bdfb93628732420620
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359864"
---
# <a name="interrupt-sync-objects"></a>割り込み同期のオブジェクト


## <span id="interrupt_sync_objects"></span><span id="INTERRUPT_SYNC_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iinterruptsync)ミニポート ドライバーのためのインターフェイス。 **IInterruptSync**以外からの割り込みルーチンと割り込みサービス ルーチン (Isr) の一覧の実行を同期する割り込み同期オブジェクトを表します。

割り込み同期オブジェクトでは、2 つの主要機能を提供します。

-   実行、割り込みに応答で isr を特定のリスト。 同期オブジェクトは、割り込みソースに接続されます。 毎回、割り込みが発生する同期オブジェクトが、選択したモードに従って、指定された順序で、Isr を実行します。 (次の 3 つのモードの説明を参照してください)。

-   Isr を特定できないルーチンの実行。 これら以外からの割り込みのルーチンは、同期オブジェクトの割り込みに接続されていません。 代わりに、呼び出し元の選択時以外からの割り込みのルーチンが実行されます。 ただし、同期オブジェクトは、isr を特定のオブジェクトの一覧で同期的に非割り込みルーチンを実行します。 つまり、非割り込みルーチンの実行が完了を実行する同期オブジェクトのリストに isr を特定のいずれかの開始前に、またはその逆です。

割り込みの同期オブジェクトは、複数の Isr を処理する柔軟性があります。 Isr を特定は、割り込み時に、同期オブジェクトを通過するリンクのリストに存在します。 ミニポート ドライバーで ISR 同期オブジェクトを登録する場合は、ISR を先頭またはこのリストの末尾に追加するかどうかを指定します。

ミニポート ドライバーは呼び出し、 [ **PcNewInterruptSync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewinterruptsync)割り込み同期オブジェクトを作成する関数。 この呼び出し中には、ドライバーは、割り込み時に isr を特定のリストを走査するオブジェクトの方法を指定します。 呼び出しには、次の表に INTERRUPTSYNCMODE 列挙定数で指定されている 3 つのオプションがサポートしています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeNormal</strong></p></td>
<td align="left"><p>STATUS_SUCCESS を返す 1 つまで、リスト内の各 ISR を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InterruptSyncModeAll</strong></p></td>
<td align="left"><p>上記の isr を特定のリターン コードに関係なく 1 回だけリストの各 ISR を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeRepeat</strong></p></td>
<td align="left"><p>一覧で、乗車を一覧の ISR 返さない STATUS_SUCCESS が発生するまでは、isr を特定のリスト全体を走査します。</p></td>
</tr>
</tbody>
</table>

 

**InterruptSyncModeNormal**モードでは、同期オブジェクトを呼び出す各 ISR リストのうち 1 つの状態を返すまで\_成功します。 この ISR に続く Isr が一覧には呼び出されません。 このモードでは、オペレーティング システムが通常 Isr を処理する方法をエミュレートします。 None、isr を特定の状態を返す場合\_成功すると、動作は同じ**InterruptSyncModeAll**します。

**InterruptSyncModeAll**モードでは、各 ISR の一覧でが呼び出される厳密に 1 回は、上記の isr を特定のリターン コードに関係なく。 これは、プリミティブではハードウェア割り込みのソースがない確定的でも、他の状況で便利ですです。 たとえば、特定の割り込みが元の 2 つのソースに関係なく、すべての割り込みで割り込みの 2 つのソースを緊密に同期可能性があります。

**InterruptSyncModeRepeat**モードでは、同期オブジェクト繰り返しはリストを走査全体 isr を特定のリストで、乗車では、ルーチンの一覧で返すにない状態が発生するまで\_成功します。 このモードは、状況、同時に同じ割り込み行に複数のソースからの割り込みが発生可能性がありますまたは ISR 処理中に 2 つ目の割り込みが発生します。 すべての割り込みのソースは、処理が必要かどうかを判断できる必要があります。 システムの状態が常に返す ISR 場合の応答が停止\_成功がこのモードでの同期オブジェクトに登録されています。

これらのモードで、同期オブジェクトは認識、割り込み、オペレーティング システムに登録されている isr を特定の状態を返す場合\_成功します。 すべての 3 つのモードで割り込みのすべてのソースを示すことが正常に処理しなかった、割り込み同期オブジェクト コードが返されます、失敗した結果、オペレーティング システムにします。

**IInterruptSync**インターフェイスは、次のメソッドをサポートしています。

[**IInterruptSync::CallSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iinterruptsync-callsynchronizedroutine)

[**IInterruptSync::Connect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iinterruptsync-connect)

[**IInterruptSync::Disconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iinterruptsync-disconnect)

[**IInterruptSync::GetKInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iinterruptsync-getkinterrupt)

[**IInterruptSync::RegisterServiceRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iinterruptsync-registerserviceroutine)

 

 




