---
title: IRP_MN_DISABLE_COLLECTION
description: 収集に負荷がかかるように1つ以上のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: de375d56-880e-4534-acab-8d0685f45ebe
keywords:
- IRP_MN_DISABLE_COLLECTION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 86c0c0faeabb963dda0b9ed8aa7ed11232e582fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828056"
---
# <a name="irp_mn_disable_collection"></a>IRP\_\_\_コレクションを無効にする


収集に負荷がかかるように1つ以上のデータブロックを登録する WMI ドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、\_コレクション要求を無効にして**IRP\_\_** を[**処理するよう**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)に呼び出した場合は、WMI によってそのドライバーの機能の[*管理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)ルーチンが呼び出されます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

この IRP は、ドライバーが収集にかかるコストとして登録され、データ収集が有効になっているデータブロックのデータの累積を停止するようにドライバーに要求するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、データの蓄積を停止するデータブロックを識別する GUID を指します。

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

ドライバーは、データブロックを登録[**または更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)するときに、ドライバーが WMI に[**渡す、wmi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)に\_\_フラグを設定することにより、収集にかかるコストとしてデータブロックを**登録します**。データブロック。 ドライバーは、コレクションを有効にするための明示的な要求を受け取るまで、このようなブロックのデータを蓄積する必要がありません。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して WMI irp を処理する場合、そのルーチンは、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合は、状態\_SUCCESS を返します。

ドライバーが IRP\_を処理し、\_コレクション要求自体を**無効\_** 場合は、パラメーターが渡された場合にのみ、ドライバーが渡さ [**れたポインターと同じデバイスオブジェクトを指すようにする必要があります。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。 データブロックが有効であるにもかかわらず、\_フラグ\_に登録されていない場合、ドライバーは正常に状態\_を返し、それ以上の操作を実行することはできません。

ドライバーは、データ収集が既に無効になっているかどうかを確認する必要はありません。これは、最後のデータコンシューマーがそのブロックのコレクションを無効にした場合に、データブロックに対して単一の無効化要求を送信するためです。 WMI は、を有効にするために介在する要求がないと、別の無効化要求を送信しません。

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

[**IRP\_\_\_コレクションを有効にする**](irp-mn-enable-collection.md)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[ **"WMI REGGUID"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




