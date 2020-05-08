---
title: IRP_MN_ENABLE_EVENTS
description: 1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 4c6012b643ca9cf5732699e7c0d843427cdbccd3
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922493"
---
# <a name="irp_mn_enable_events"></a>IRP\_が\_有効\_になっているイベント


1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、このドライバーの**\_\_\_イベント**要求を処理するために、呼び出し[*元の wmi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback) [**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出す場合、WMI はそのドライバーの機能を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、データコンシューマーがイベントの通知を要求したことをドライバーに通知するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、有効にするイベントブロックを識別する GUID を指します。

**パラメーター.** Wmi. BufferSize は、非ページバッファーのサイズを示します。この**バッファー**は**sizeof**(**\_wnode HEADER**) 以上である必要があります。 トレースブロックが登録されていないドライバー (\_この\_場合\_は、wmi フラグがトレースされた GUID) は、このパラメーターを無視できます。

**パラメーター。 wmi**は、イベントをトレースする (wmi\_フラグ\_トレース\_された GUID) かどうかを示す**wnode\_ヘッダー**を指し、システムロガーへのハンドルを提供します。 トレースブロックが登録されていないドライバー (\_この\_場合\_は、wmi フラグがトレースされた GUID) は、このパラメーターを無視できます。

## <a name="output-parameters"></a>出力パラメーター


ありません。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

状態\_WMI\_GUID\_が\_見つかりません

デバイス\_\_要求\_の状態が無効です

成功した場合、ドライバーは**Irp&gt;-Iostatus. 情報**をゼロに設定します。

<a name="operation"></a>Operation
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが WMI Irp を処理するとき[**に、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンによって、Wmi の irp が処理される場合、そのルーチン\_は、ドライバーの状態を呼び出します。または、ドライバーがルーチンを定義していない場合は、[*成功の状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を返します。

ドライバーが**IRP\_が発生\_する\_イベント**の要求を処理する場合は、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指す場合にのみ、そのようにする必要があり**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーが要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーでイベントブロックがサポートされている場合、そのデータブロックのすべてのインスタンスに対してイベントが有効になります。

イベントブロックに対してイベントが既に有効になっているかどうかをドライバーが確認する必要はありません。これは、最初のデータコンシューマーがイベントを有効にするときに、イベントブロックに対してを有効にする単一の要求を送信するからです。 WMI は、介在する無効化要求なしに、有効にする別の要求を送信しません。

トレースブロックを登録するドライバー (この場合\_は\_、\_wmi フラグがトレースされた GUID) は、WMI にイベントを送信するか、トレース用にシステムロガーに送信するかを決定する必要があります。 トレースが要求された場合、パラメーターは[**\_wnode ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)構造をポイントし**ます。** これは、**フラグ**が\_wnode\_フラグ\_で設定され、トレースされた GUID と**HistoricalContext**に logger のハンドルが含まれていることを示します。

イベントブロックの定義、イベントの送信、およびトレースの詳細については、「 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)」を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*\N 関数コントロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_の\_全\_無効化イベント**](irp-mn-disable-events.md)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_イベント\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)

[**WNODE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)

 

 




