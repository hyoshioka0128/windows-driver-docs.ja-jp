---
title: IRP_MN_DISABLE_EVENTS
description: 1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 3187643b-27d7-4a6d-8fbe-4f8eb6c251ed
keywords:
- IRP_MN_DISABLE_EVENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 8672d4360f2aaa1dc301c00404a495870bd148e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838587"
---
# <a name="irp_mn_disable_events"></a>IRP\_\_\_イベントを無効にする


1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **\_EVENTS\_を無効**にして、IRP\_[**を処理するよう**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)に呼び出した場合、WMI はその[*ドライバーの機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、この IRP を送信して、データコンシューマーがイベントについてのそれ以上の通知を要求していないことをドライバーに通知します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、無効にするイベントブロックを識別する GUID を指します。

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

ドライバーが IRP\_を処理し、 **\_イベント**の要求自体を無効に\_場合は、ドライバーが渡さ [**れたポインターと同じデバイスオブジェクトを指定している場合にのみ、この操作を行う必要があります。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーがイベントブロックをサポートしている場合は、そのブロックのすべてのインスタンスのイベントを無効にします。

このイベントブロックのイベントが既に無効になっているかどうかをドライバーが確認する必要はありません。これは、最後のデータコンシューマーがイベントを無効にしたときに、そのイベントブロックに対して1つの無効化要求が送信されるためです。 WMI は、を有効にするために介在する要求がないと、別の無効化要求を送信しません。

イベントブロックの定義の詳細については、「 [WMI データおよびイベントブロックのデザイン](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)」を参照してください。

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


[ *\N 関数コントロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_\_\_イベントを有効にする**](irp-mn-enable-events.md)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




