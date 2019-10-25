---
title: 割り込み同期のオブジェクト
description: 割り込み同期のオブジェクト
ms.assetid: c9e228e0-6178-442d-a82a-6b14ed67c9d2
keywords:
- ヘルパーオブジェクト WDK オーディオ、割り込み同期オブジェクト
- interrupt sync オブジェクト WDK audio
- IInterruptSync インターフェイス
- WDK オーディオの同期
- 割り込みサービスルーチン WDK オーディオ
- Isr WDK オーディオ
- 非割り込みルーチン WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27065946638fe81450cdc49ebae2cf35d721bab3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833207"
---
# <a name="interrupt-sync-objects"></a>割り込み同期のオブジェクト


## <span id="interrupt_sync_objects"></span><span id="INTERRUPT_SYNC_OBJECTS"></span>


PortCls システムドライバーは、ミニポートドライバーの利点を得るために[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync)インターフェイスを実装しています。 **IInterruptSync**は、割り込みサービスルーチン (isr) の一覧の実行を非割り込みルーチンと同期する割り込み同期オブジェクトを表します。

割り込み同期オブジェクトは、次の2つの主要な機能を提供します。

-   割り込みに対する応答としての Isr の一覧の実行。 同期オブジェクトは割り込みソースに接続されています。 同期オブジェクトは、割り込みが発生するたびに、選択されたモードに従って、指定された順序で Isr を実行します。 (3 つのモードについては、次の説明を参照してください)。

-   Isr ではないルーチンの実行。 これらの非割り込みルーチンは、同期オブジェクトの割り込みに接続されていません。 代わりに、割り込み以外のルーチンは、呼び出し元が選択したときに実行されます。 ただし、同期オブジェクトは、オブジェクトの Isr のリストを使用して、非割り込みルーチンを同期的に実行します。 つまり、非割り込みルーチンは、同期オブジェクトのリスト内のいずれかの Isr の実行が開始される前に完了するように実行されます。その逆も同様です。

割り込み同期オブジェクトは、複数の Isr を処理するのに柔軟です。 Isr は、同期オブジェクトが割り込み時間に通過するリンクリストに存在します。 ミニポートドライバーが ISR を同期オブジェクトに登録する場合は、このリストの先頭または末尾に ISR を追加する必要があるかどうかを指定します。

ミニポートドライバーは、 [**PcNewInterruptSync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewinterruptsync)関数を呼び出して、割り込み同期オブジェクトを作成します。 この呼び出しの間に、ドライバーは、割り込み時にオブジェクトが Isr の一覧を走査する方法を指定します。 この呼び出しでは、次の表の INTERRUPTSYNCMODE 列挙定数で指定される3つのオプションがサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeNormal</strong></p></td>
<td align="left"><p>リスト内の各 ISR は、そのいずれかが STATUS_SUCCESS を返すまで呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InterruptSyncModeAll</strong></p></td>
<td align="left"><p>前の Isr のリターンコードに関係なく、リスト内の各 ISR を1回だけ呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeRepeat</strong></p></td>
<td align="left"><p>リスト内の ISR が STATUS_SUCCESS を返さないようになるまで、Isr のリスト全体を走査します。</p></td>
</tr>
</tbody>
</table>

 

**InterruptSyncModeNormal**モードでは、同期オブジェクトは、そのいずれかが状態\_SUCCESS を返すまで一覧内の各 ISR を呼び出します。 この ISR に従うリスト内のすべての Isr は呼び出されません。 このモードは、通常、オペレーティングシステムが Isr を処理する方法をエミュレートします。 Isr が正常に\_返されない場合、の動作は**InterruptSyncModeAll**と同じになります。

**InterruptSyncModeAll**モードでは、リスト内の各 ISR は、前の isr のリターンコードに関係なく、1回だけ呼び出されます。 これは、割り込みの原因が決定的ではない、より多くのプリミティブハードウェアを対象としていますが、他の状況でも役に立つ可能性があります。 たとえば、2つの割り込みソースは、特定の割り込みの原因となる2つのソースのいずれかに関係なく、すべての割り込みで緊密に同期されている可能性があります。

**InterruptSyncModeRepeat**モードでは、リスト内のルーチンによって状態\_SUCCESS が返されないようにするために、同期オブジェクトは isr のリスト全体を繰り返し走査します。 このモードは、複数のソースからの割り込みが同時に同じ割り込み回線で発生する場合や、ISR の処理中に2つ目の割り込みが発生する場合に適しています。 すべての割り込みソースは、処理が必要かどうかを判断できなければなりません。 常にステータス\_成功した ISR がこのモードで同期オブジェクトに登録されている場合、システムは応答を停止します。

これらのいずれかのモードでは、登録されている Isr の戻り状態\_成功した場合、同期オブジェクトはオペレーティングシステムへの割り込みを認識します。 3つのモードでは、すべての割り込みソースによって割り込みが正常に処理されなかったことが示された場合、同期オブジェクトは失敗した結果コードをオペレーティングシステムに返します。

**IInterruptSync**インターフェイスは、次のメソッドをサポートしています。

[**IInterruptSync::CallSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-callsynchronizedroutine)

[**IInterruptSync:: Connect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-connect)

[**IInterruptSync::D isconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-disconnect)

[**IInterruptSync:: GetKInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-getkinterrupt)

[**IInterruptSync:: RegisterServiceRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-registerserviceroutine)

 

 




