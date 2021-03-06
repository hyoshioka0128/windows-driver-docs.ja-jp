---
title: IRP_MJ_SYSTEM_CONTROL
description: すべてのドライバーでは、Windows Management Instrumentation (WMI) のカーネル モード コンポーネントが送信する IRP_MJ_SYSTEM_CONTROL 要求を処理する DispatchSystemControl ルーチンを指定する必要があります。
ms.date: 08/12/2017
ms.assetid: 1b4dfc87-3f74-4e33-9dbb-72d4f72480fc
keywords:
- IRP_MJ_SYSTEM_CONTROL Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 17a74a7029b8130f31a1abadf4dd3aaf7a7d2d99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382256"
---
# <a name="irpmjsystemcontrol"></a>IRP\_MJ\_SYSTEM\_CONTROL


すべてのドライバーを提供する必要があります、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)処理ルーチン**IRP\_MJ\_システム\_コントロール**要求でのカーネル モード コンポーネントによって送信が[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI)。

<a name="when-sent"></a>送信時
---------

WMI のカーネル モード コンポーネントに送信できる、 **IRP\_MJ\_システム\_コントロール**WMI データの供給業者として次のドライバーの登録に成功した任意の時間を要求します。 WMI Irp 通常が送信されるユーザー モードのデータ コンシューマーが WMI データを要求されたときにします。

## <a name="input-parameters"></a>入力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。 すべて**IRP\_MJ\_システム\_コントロール**要求が要求された WMI 操作を識別するマイナー関数コードを指定します。

## <a name="output-parameters"></a>出力パラメーター


値に依存**MinorFunction**現在 I/O スタック IRP の場所。

<a name="operation"></a>操作
---------

すべてのドライバーをサポートする必要があります**IRP\_MJ\_システム\_コントロール**要求を指定することによって、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン.

サポートするドライバー [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) を処理する必要があります**IRP\_MJ\_システム\_コントロール**マイナー関数を処理することによって要求この主な機能のコードに関連付けられたコードです。 WMI のマイナー関数コードの詳細については、次を参照してください。 [WMI マイナー Irp](wmi-minor-irps.md)します。

ドライバーで WMI をサポートしていない[WMI データ プロバイダーとして登録する](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-as-a-wmi-data-provider)渡す必要があります**IRP\_MJ\_システム\_コントロール**[次へ] の下のドライバーに要求します。

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


[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




