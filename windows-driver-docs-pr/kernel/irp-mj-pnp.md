---
title: IRP_MJ_PNP
description: すべてのドライバーは、DispatchPnP ルーチンで IRP_MJ_PNP 要求を処理するために準備する必要があります。
ms.date: 08/12/2017
ms.assetid: db838761-b838-44fd-bc77-c9d55d2c4a41
keywords:
- IRP_MJ_PNP カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 50bb59535a4cd7726b8e490b910e22d621f4d47f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838601"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでは、すべてのドライバーが**IRP\_MJ\_PNP**要求を処理できるように準備する必要があります。

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、列挙、リソースの再調整、およびシステムでプラグアンドプレイアクティビティが発生するその他のすべての時間に、 **IRP\_MJ\_pnp**要求を送信します。 ドライバーは、マイナー関数コードに応じて、特定の**IRP\_MJ\_PNP**要求を送信することもできます。

## <a name="input-parameters"></a>入力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。 すべての**IRP\_MJ\_PNP**要求は、要求された PNP アクションを識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。

<a name="operation"></a>操作
---------

**Irp\_MJ\_PNP**要求の詳細については、「[プラグアンドプレイ Minor irp](plug-and-play-minor-irps.md) 」を参照してください。

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


[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




