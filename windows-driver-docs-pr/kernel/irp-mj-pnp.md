---
title: IRP_MJ_PNP
description: DispatchPnP ルーチンで IRP_MJ_PNP 要求をサービスには、すべてのドライバーを準備する必要があります。
ms.date: 08/12/2017
ms.assetid: db838761-b838-44fd-bc77-c9d55d2c4a41
keywords:
- IRP_MJ_PNP Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: eeaf4ba1c289f3fa4aaa84bc14f9f0f758a7c6b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539038"
---
# <a name="irpmjpnp"></a>IRP\_MJ\_PNP


すべてのドライバーは、サービスを準備する必要があります**IRP\_MJ\_PNP**で要求を[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

<a name="when-sent"></a>送信時
---------

PnP マネージャー送信**IRP\_MJ\_PNP**列挙型、リソースが再分配、およびその他の時刻のプラグ アンド プレイ活動中に要求が、システムで発生します。 ドライバーも送信できる特定**IRP\_MJ\_PNP**マイナー関数コードによって、要求。

## <a name="input-parameters"></a>入力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。 すべて**IRP\_MJ\_PNP**要求が要求された PnP アクションを識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。

<a name="operation"></a>操作
---------

参照してください[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)の詳細については**IRP\_MJ\_PNP**要求。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




