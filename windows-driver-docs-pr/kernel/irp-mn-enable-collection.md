---
title: IRP_MN_ENABLE_COLLECTION
description: この IRP を処理する必要がある可能性が高い、または高価であると考えられる、1つまたは複数のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: dc6c3ceb-a992-4e7b-ab25-d91c00af655a
keywords:
- IRP_MN_ENABLE_COLLECTION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 6c00a2ebcb7ae8dac8ad5dfcbeec1e3a7106e584
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838583"
---
# <a name="irp_mn_enable_collection"></a>IRP\_\_\_コレクションを有効にする


この IRP を処理する必要がある可能性が高い、または*高価*であると考えられる、1つまたは複数のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **\_COLLECTION 要求\_有効**に[**するために**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)、wmi を呼び出して、IRP\_を処理する場合、WMI はその[*ドライバーの機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、この IRP を送信して、ドライバーが収集にかかるコストとして登録されたデータブロックのデータの累積を開始するようにドライバーに要求します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、データが蓄積されるデータブロックを識別する GUID を指します。

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

ドライバーは、データブロックを収集するのにコストが高いとして登録します。これを行うに[**は、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw) **\_\_フラグ**を設定します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo) ドライバーは、データブロックを登録または更新するときに、これらの構造体を WMI に渡します。 ドライバーは、データ収集を開始するための明示的な要求を受信するまで、このようなブロックのデータを蓄積する必要がありません。

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して WMI irp を処理する場合、そのルーチンは、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合は、状態\_SUCCESS を返します。

ドライバーが IRP\_を処理して **\_コレクション要求自体\_有効**にする場合は、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡されたポインターと同じデバイスオブジェクトを指す場合にのみ、このように**します。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

要求を処理する前に、ドライバーは、**データパス**がドライバーがサポートしている GUID を指していることを確認する必要があります。 そうでない場合は、ドライバーが IRP を失敗させ、ステータス\_WMI\_GUID\_見つから\_ないことを確認します。 データブロックが有効であるにもかかわらず、\_フラグ\_に登録されていない場合、ドライバーは正常に状態\_を返し、それ以上の操作を実行することはできません。

ブロックが有効であり、また、\_フラグ\_に登録されている場合、ドライバーはそのデータブロックのすべてのインスタンスに対してデータ収集を有効にします。

データブロックに対してデータ収集が既に有効になっているかどうかをドライバーが確認する必要はありません。 WMI は、最初のデータコンシューマーがブロックを有効にした後にデータブロックを有効にするために、1つの要求だけを送信します。 WMI は、介在する無効化要求なしに、有効にする別の要求を送信しません。

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

[**IRP\_\_\_コレクションを無効にする**](irp-mn-disable-collection.md)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[ **"WMI REGGUID"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




