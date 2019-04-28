---
title: IRP_MJ_FLUSH_BUFFERS
description: データの内部キャッシュを使用したデバイスのドライバーとドライバーのデータの内部バッファーを維持するには、DispatchFlushBuffers ルーチンでは、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: c1023999-0c80-4c09-a9ea-a9422184bba7
keywords:
- IRP_MJ_FLUSH_BUFFERS カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: dafd90b42a77ddaa816278fd6b484ce6a664d6f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368518"
---
# <a name="irpmjflushbuffers"></a>IRP\_MJ\_フラッシュ\_バッファー


データとデータでこの要求を処理する必要がありますの内部バッファーを維持するドライバーの内部キャッシュを持つデバイスのドライバーを[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

<a name="when-sent"></a>送信時
---------

フラッシュの要求の受信は、ドライバーがデバイスのキャッシュまたは内部バッファーをフラッシュする必要がありますか、場合によっては、内部バッファー内のデータを破棄する必要があることを示します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、現在、デバイスにキャッシュされているか、フラッシュの要求を完了する前に、ドライバーの内部バッファーに保持されているすべてのデータを転送します。 ドライバーを専用デバイス内部的にデータ バッファーに格納する可能性があります単にデータを破棄現在バッファリングされているデバイス、デバイスの性質によって、フラッシュの IRP を完了する前にします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




