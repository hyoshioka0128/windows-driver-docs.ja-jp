---
title: IRP_MJ_POWER
description: すべてのドライバーは、DispatchPower ルーチンで IRP_MJ_POWER 要求を処理するために準備する必要があります。
ms.date: 08/12/2017
ms.assetid: ca53ceef-2755-49d3-aab9-0d12a0e51e75
keywords:
- IRP_MJ_POWER カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 7ebe72a1d26fdd9196f9f0cc6eac3b3784d2829b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828104"
---
# <a name="irp_mj_power"></a>IRP\_MJ\_POWER


[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでは、すべてのドライバーが**IRP\_MJ\_の電源**要求を処理できるように準備する必要があります。

<a name="when-sent"></a>送信時
---------

電源マネージャーまたはドライバーは、オペレーティングシステムが実行されているときに、いつでも**IRP\_MJ\_の電源**要求を送信できます。

## <a name="input-parameters"></a>入力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。 すべての**IRP\_MJ\_の電源**要求は、要求された電源操作を識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。

<a name="operation"></a>操作
---------

Irp の処理を制御する通常のルールに加えて、 **irp\_MJ\_電源**irp には次の特別な要件があります。電源 irp を受信するドライバーは、の i/o スタックの場所にあるメジャーおよびマイナー関数のコードを変更することはできません。電源マネージャーまたは上位レベルのドライバーによって設定された IRP。 これらの関数コードは、IRP が完了するまで変更されません。 この規則に違反すると、デバッグが困難な問題が発生する可能性があります。 たとえば、オペレーティングシステムが応答を停止したり、"ハング" したりする可能性があります。

**IRP\_MJ\_の電源**要求の詳細については、「[電源管理の小さな irp](power-management-minor-irps.md) 」を参照してください。

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


[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




