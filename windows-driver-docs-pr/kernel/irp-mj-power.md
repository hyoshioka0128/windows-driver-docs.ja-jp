---
title: IRP_MJ_POWER
description: DispatchPower ルーチンに対し、IRP_MJ_POWER 要求をサービスには、すべてのドライバーを準備する必要があります。
ms.date: 08/12/2017
ms.assetid: ca53ceef-2755-49d3-aab9-0d12a0e51e75
keywords:
- IRP_MJ_POWER Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 0355a600ffe5ebd9e27358c95106966727382f5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368470"
---
# <a name="irpmjpower"></a>IRP\_MJ\_POWER


すべてのドライバーは、サービスを準備する必要があります**IRP\_MJ\_POWER**で要求を[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

<a name="when-sent"></a>送信時
---------

電源マネージャーまたはドライバーに送信できる**IRP\_MJ\_POWER**オペレーティング システムが実行されている、いつでも要求。

## <a name="input-parameters"></a>入力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。 すべて**IRP\_MJ\_POWER**要求が要求された電源操作を識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。

<a name="operation"></a>操作
---------

Irp の処理を制御する通常の規則だけでなく**IRP\_MJ\_POWER** Irp に次の特別な要件があります。累乗を受け取るドライバー IRP では、I/O スタック内の場所に IRP 電源マネージャーによって、またはより高度なドライバーに設定されているメジャーおよびマイナーの関数コードを変更しないでください。 電源マネージャーは IRP が完了するまでそのまま残り、これらの関数コードに依存します。 この規則の違反をデバッグするが困難な問題が発生することができます。 たとえば、オペレーティング システムを応答を停止または「ハング」可能性があります。

参照してください[電源管理のマイナー Irp](power-management-minor-irps.md)の詳細については**IRP\_MJ\_POWER**要求。

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


[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




