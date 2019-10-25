---
title: IRP_MJ_FLUSH_BUFFERS
description: データ用の内部キャッシュを持つデバイスのドライバーと、データの内部バッファーを保持するドライバーは、DispatchFlushBuffers ルーチンでこの要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: c1023999-0c80-4c09-a9ea-a9422184bba7
keywords:
- IRP_MJ_FLUSH_BUFFERS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 4aaa0a47ad4cd013883d5d1b988f026791bac342
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838605"
---
# <a name="irp_mj_flush_buffers"></a>IRP\_MJ\_フラッシュ\_バッファー


データ用の内部キャッシュを持つデバイスのドライバーと、データの内部バッファーを保持するドライバーは、 [*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでこの要求を処理する必要があります。

<a name="when-sent"></a>送信時
---------

フラッシュ要求の受信は、ドライバーがデバイスのキャッシュまたは内部バッファーをフラッシュする必要があること、または内部バッファー内のデータを破棄する必要があることを示します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、フラッシュ要求を完了する前に、デバイスに現在キャッシュされているデータ、またはドライバーの内部バッファーに保持されているすべてのデータを転送します。 内部的にデータをバッファーする入力のみのデバイスのドライバーは、デバイスの性質に応じて、フラッシュ IRP を完了する前に現在バッファーされているデバイスデータを破棄するだけで済みます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




