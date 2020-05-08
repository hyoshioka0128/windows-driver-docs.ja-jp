---
title: IRP_MN_DISABLE_EVENTS
description: 1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 3187643b-27d7-4a6d-8fbe-4f8eb6c251ed
keywords:
- IRP_MN_DISABLE_EVENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: ebd4065ac28c3124f60c70e295d6fdd2c7f55e96
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922471"
---
# <a name="irp_mn_disable_events"></a>IRP\_の\_全\_無効化イベント


1つ以上のイベントブロックを登録するすべての WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが呼び出し元の**\_\_\_イベント**要求を処理するために、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すと、WMI はその[*ドライバーの機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、この IRP を送信して、データコンシューマーがイベントについてのそれ以上の通知を要求していないことをドライバーに通知します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、無効にするイベントブロックを識別する GUID を指します。

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

ドライバーが**IRP\_\_による無効\_なイベント**の要求自体を処理する場合は、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡されたポインターと同じデバイスオブジェクトを指す場合にのみ、そのようにする必要があり**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーがイベントブロックをサポートしている場合は、そのブロックのすべてのインスタンスのイベントを無効にします。

このイベントブロックのイベントが既に無効になっているかどうかをドライバーが確認する必要はありません。これは、最後のデータコンシューマーがイベントを無効にしたときに、そのイベントブロックに対して1つの無効化要求が送信されるためです。 WMI は、を有効にするために介在する要求がないと、別の無効化要求を送信しません。

イベントブロックの定義の詳細については、「 [WMI データおよびイベントブロックのデザイン](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)」を参照してください。

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

[**IRP\_が\_有効\_になっているイベント**](irp-mn-enable-events.md)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




