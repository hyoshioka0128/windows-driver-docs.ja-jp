---
title: IRP_MN_ENABLE_EVENTS
description: 1 つまたは複数のイベント ブロックを登録する任意の WMI ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 84874bbd689040f0580393ce0f79b59317775eed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353367"
---
# <a name="irpmnenableevents"></a>IRP\_MN\_を有効にする\_イベント


1 つまたは複数のイベント ブロックを登録する任意の WMI ドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)処理するために、 **IRP\_MN\_を有効にする\_イベント**WMI がさらに呼び出しを要求します。ドライバーの[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、この IRP データ コンシューマーがイベントの通知を要求したことをドライバーに通知を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**を有効にする、イベント ブロックを識別する GUID を指します。

**Parameters.WMI.BufferSize** nonpaged、バッファーのサイズを示します**Parameters.WMI.Buffer**、以上にする必要があります、 **sizeof**(**れた WNODE\_ヘッダー**)。 ドライバーのトレースのブロックを登録できません (WMIREG\_フラグ\_追跡\_GUID) このパラメーターは無視してかまいません。

**Parameters.WMI.Buffer**を指す、**れた WNODE\_ヘッダー**イベントをトレースするかどうかを示す (WMI\_フラグ\_追跡\_GUID) と、ハンドルを提供しますシステムのログにします。 ドライバーのトレースのブロックを登録できません (WMIREG\_フラグ\_追跡\_GUID) このパラメーターは無視してかまいません。

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

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、ドライバーが、ルーチンを呼び出す[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)ルーチン状態を取得または\_ドライバーは、ルーチンを定義していない場合は成功します。

ドライバーが処理する場合、 **IRP\_MN\_を有効にする\_イベント**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**として同じデバイス オブジェクトを指し示すドライバーに渡されたポインター [ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

ドライバーは、要求を処理する前に確認する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

ドライバーは、イベント ブロックをサポートする場合は、そのデータ ブロックのすべてのインスタンスのイベントを使用できます。

WMI は、最初のデータ コンシューマーがイベントを有効に、イベント ブロックを有効にする 1 つの要求を送信するため、イベントがイベント ブロックを有効既にかどうかを確認するドライバーの必要はありません。 WMI は、その前の要求を無効にすることがなく有効にする別の要求を送信しません。

トレースのブロックを登録するドライバー (WMIREG\_フラグ\_追跡\_GUID) も WMI またはシステムのログにトレースのイベントを送信するかどうかを決定する必要があります。 トレースが要求された場合**Parameters.WMI.Buffer**を指す、 [**れた WNODE\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-_wnode_header)構造の**フラグ**はれた WNODE セット\_フラグ\_追跡\_GUID と**HistoricalContext**ロガーへのハンドルが含まれています。

イベント ブロックを定義する方法については、送信側のイベント、およびトレースを参照してください[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)します。

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

[**IRP\_MN\_を無効にする\_イベント**](irp-mn-disable-events.md)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**れた WNODE\_イベント\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_event_item)

[**れた WNODE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-_wnode_header)

 

 




