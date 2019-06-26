---
title: IRP_MN_DISABLE_COLLECTION
description: 任意の WMI ドライバーを収集する高価なとしてそのデータ ブロックの 1 つ以上を登録するには、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: de375d56-880e-4534-acab-8d0685f45ebe
keywords:
- IRP_MN_DISABLE_COLLECTION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 6a8f51015af90accfd378859c774b656374610bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353371"
---
# <a name="irpmndisablecollection"></a>IRP\_MN\_を無効にする\_コレクション


任意の WMI ドライバーを収集する高価なとしてそのデータ ブロックの 1 つ以上を登録するには、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)処理するために、 **IRP\_MN\_を無効にする\_コレクション**要求、WMI が呼び出されますドライバーの[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、累積データとして収集する高価なドライバーが登録されているデータ ブロックとどのデータ収集を有効になっているを停止するドライバーを要求するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**データの蓄積を停止するか、データ ブロックを識別する GUID を指します。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_無効な\_デバイス\_要求

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

ドライバーでは、データ ブロックを登録 WMIREG を設定して、収集する高価なとして\_フラグ\_高コストで、**フラグ**のメンバー、 [ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)または[ **WMIGUIDREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)登録またはデータ ブロックを更新するときに、ドライバーが WMI に渡される構造体。 コレクションを有効にする明示的な要求を受信するまで、ドライバーはこのようなブロックのデータを収集しない必要があります。

ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、ドライバーが、ルーチンを呼び出す[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)ルーチン状態を取得または\_ドライバーは、ルーチンを定義していない場合は成功します。

ドライバーが処理する場合、 **IRP\_MN\_を無効にする\_コレクション**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**同じデバイスを指しますオブジェクトに、ドライバーが渡されたポインターとして[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。 データ ブロックは有効ですが、なかった場合は、WMIREG に登録されている\_フラグ\_高コストで、ドライバーは状態を返すことができます\_成功し、さらに操作は不要です。

WMI は、最後のデータ コンシューマーがそのブロックのコレクションを無効にされた場合にデータ ブロックの 1 つの無効化要求を送信するため、データ コレクションが既に無効にするかどうかを確認するドライバーの必要はありません。 WMI は、介在する要求を有効にすることがなく別の無効化要求を送信しません。

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


[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_MN\_ENABLE\_COLLECTION**](irp-mn-enable-collection.md)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)

[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

 

 




