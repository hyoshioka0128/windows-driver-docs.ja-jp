---
title: IRP_MJ_SYSTEM_CONTROL
description: すべてのドライバーは、DispatchSystemControl ルーチンを提供する必要があります。これは、Windows Management Instrumentation (WMI) のカーネルモードコンポーネントによって送信される IRP_MJ_SYSTEM_CONTROL 要求を処理します。
ms.date: 08/12/2017
ms.assetid: 1b4dfc87-3f74-4e33-9dbb-72d4f72480fc
keywords:
- IRP_MJ_SYSTEM_CONTROL カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 711a11b7494461bb5c290321e0622b3ea88443e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828101"
---
# <a name="irp_mj_system_control"></a>IRP\_MJ\_SYSTEM\_CONTROL


すべてのドライバーは、 **IRP\_MJ\_システム\_制御**要求を処理する[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを提供する必要があります。これは、 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) のカーネルモードコンポーネントによって送信されます。

<a name="when-sent"></a>送信時
---------

Wmi カーネルモードコンポーネントは、WMI データの供給元としてドライバーが正常に登録された後、いつでも**IRP\_MJ\_SYSTEM\_CONTROL**要求を送信できます。 通常、WMI Irp は、ユーザーモードデータコンシューマーが WMI データを要求したときに送信されます。

## <a name="input-parameters"></a>入力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。 すべての**IRP\_MJ\_SYSTEM\_CONTROL**要求では、要求された WMI アクションを識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


は、IRP の現在の i/o スタック位置にある**Minorfunction**の値に依存します。

<a name="operation"></a>操作
---------

すべてのドライバーは、 [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを指定することによって、 **IRP\_MJ\_システム\_制御**要求をサポートする必要があります。

[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) をサポートするドライバーは、この主要な関数コードに関連付けられているマイナー関数コードを処理することによって、 **IRP\_MJ\_システム\_制御**要求を処理する必要があります。 WMI のマイナー関数コードの詳細については、「 [Wmi Minor irp](wmi-minor-irps.md)」を参照してください。

Wmi[データプロバイダーとして登録](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-as-a-wmi-data-provider)することによって wmi をサポートしていないドライバーは、 **IRP\_MJ\_SYSTEM\_制御**要求を次の下位のドライバーに渡す必要があります。

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


[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




