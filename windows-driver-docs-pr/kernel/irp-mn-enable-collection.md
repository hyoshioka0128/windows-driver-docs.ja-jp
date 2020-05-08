---
title: IRP_MN_ENABLE_COLLECTION
description: この IRP を処理する必要がある可能性が高い、または高価であると考えられる、1つまたは複数のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: dc6c3ceb-a992-4e7b-ab25-d91c00af655a
keywords:
- IRP_MN_ENABLE_COLLECTION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 363b4899c818ec6617b51bbca0956f8ad5d147f7
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922489"
---
# <a name="irp_mn_enable_collection"></a>IRP\_が\_有効\_になっているコレクション


この IRP を処理する必要がある可能性が高い、または*高価*であると考えられる、1つまたは複数のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、要求に応じた**\_\_有効\_なコレクション**要求を[**処理するため**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)に、呼び出し元のコントロールを呼び出す場合、WMI はその[*ドライバーの機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、この IRP を送信して、ドライバーが収集にかかるコストとして登録されたデータブロックのデータの累積を開始するようにドライバーに要求します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、データが蓄積されるデータブロックを識別する GUID を指します。

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

ドライバーは、データブロックを収集のコストが高いものとし\_て\_登録します。これを行うには、[ [**wmi regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw) ] または [ [**wmiguidreginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo) ] 構造体の Flags メンバーに [の**フラグ**] を設定します。 ドライバーは、データブロックを登録または更新するときに、これらの構造体を WMI に渡します。 ドライバーは、データ収集を開始するための明示的な要求を受信するまで、このようなブロックのデータを蓄積する必要がありません。

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが WMI Irp を処理するとき[**に、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンによって、Wmi の irp が処理される場合、そのルーチン\_は、ドライバーの状態を呼び出します。または、ドライバーがルーチンを定義していない場合は、[*成功の状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を返します。

ドライバーで**IRP\_\_が有効\_なコレクション**の要求を処理する場合は、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡されたポインターと同じデバイスオブジェクトを指す場合にのみ、この操作を行う必要があり**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

要求を処理する前に、ドライバーは、**データパス**がドライバーがサポートしている GUID を指していることを確認する必要があります。 そうでない場合は、ドライバーが IRP を失敗させ、\_ステータス\_WMI\_GUID\_が見つからないことを返します。 データブロックが有効であるにもかかわら\_\_ず、そのデータブロックがの場合は、"成功\_" の状態が返されます。

ブロックが有効であり、また、このブロックが\_に\_登録されている場合は、そのデータブロックのすべてのインスタンスに対してデータ収集が有効になります。

データブロックに対してデータ収集が既に有効になっているかどうかをドライバーが確認する必要はありません。 WMI は、最初のデータコンシューマーがブロックを有効にした後にデータブロックを有効にするために、1つの要求だけを送信します。 WMI は、介在する無効化要求なしに、有効にする別の要求を送信しません。

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

[**IRP\_の\_全\_無効化のコレクション**](irp-mn-disable-collection.md)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**"WMI REGGUID"**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




