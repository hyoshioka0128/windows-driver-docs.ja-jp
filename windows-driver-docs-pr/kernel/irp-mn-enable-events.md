---
title: IRP_MN_ENABLE_EVENTS
description: 1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 0395173ac5d7b52f109d3b98ac55e345f7ea074b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838582"
---
# <a name="irp_mn_enable_events"></a>IRP\_\_\_イベントを有効にする


1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **\_EVENTS 要求\_有効**にするために、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出して、イベントの要求を有効にすると、WMI はその[*ドライバーの機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)の\_を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、データコンシューマーがイベントの通知を要求したことをドライバーに通知するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、有効にするイベントブロックを識別する GUID を指します。

**パラメーター.** Wmi. BufferSize は、非ページバッファーのサイズを示します。この**バッファー**は**SIZEOF**(**wnode\_HEADER**) 以上である必要があります。 トレースブロックが登録されていないドライバー (\_WMI\_GUID\_) は、このパラメーターを無視できます。

**パラメーター。 wmi**は、イベントをトレースする (WMI\_FLAGS\_トレースされた\_GUID) かどうかを示す**WNODE\_ヘッダー**を指し、システムロガーへのハンドルを提供します。 トレースブロックが登録されていないドライバー (\_WMI\_GUID\_) は、このパラメーターを無視できます。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

ステータス\_WMI\_GUID\_見つかりませんでした\_

デバイス\_要求\_状態\_無効です

成功した場合、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して WMI irp を処理する場合、そのルーチンは、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合は、状態\_SUCCESS を返します。

ドライバーが IRP\_を処理し、\_イベントの要求自体を**有効に\_** 場合は、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡されたポインターと同じデバイスオブジェクトを指す場合にのみ、そのように**します。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーが要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーでイベントブロックがサポートされている場合、そのデータブロックのすべてのインスタンスに対してイベントが有効になります。

イベントブロックに対してイベントが既に有効になっているかどうかをドライバーが確認する必要はありません。これは、最初のデータコンシューマーがイベントを有効にするときに、イベントブロックに対してを有効にする単一の要求を送信するからです。 WMI は、介在する無効化要求なしに、有効にする別の要求を送信しません。

トレースブロック\_(\_トレース\_GUID) を登録するドライバーは、WMI にイベントを送信するか、トレース用にシステムロガーに送信するかを決定する必要もあります。 トレースが要求された場合、パラメーターは[**wnode\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)構造体をポイントし**ます。** この構造では、**フラグ**が WNODE\_フラグ\_\_トレースされます。これにより、GUID と**HistoricalContext**には、lnm.

イベントブロックの定義、イベントの送信、およびトレースの詳細については、「 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)」を参照してください。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[ *\N 関数コントロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_\_\_イベントを無効にする**](irp-mn-disable-events.md)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_イベント\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)

[**WNODE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)

 

 




