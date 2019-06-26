---
title: IRP_MN_CHANGE_SINGLE_ITEM
description: WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9839ebb2-31a9-4cb0-adbf-1882583849fc
keywords:
- IRP_MN_CHANGE_SINGLE_ITEM Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 33a91f80058f3c5f75fd597aacb125c30d3ed9a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382239"
---
# <a name="irpmnchangesingleitem"></a>IRP\_MN\_変更\_単一\_項目


WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)処理するために、 **IRP\_MN\_変更\_単一\_項目**要求WMI を呼び出してドライバーの[ *DpWmiSetDataItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、データ ブロックの 1 つのインスタンスで 1 つのデータ項目を変更するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**を設定するデータ ブロックを識別する GUID を指します。

**Parameters.WMI.BufferSize** nonpaged、バッファーのサイズを示します**Parameters.WMI.Buffer**します。

**Parameters.WMI.Buffer**、指す、 [**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)データのインスタンスを識別する構造体ブロックを設定する項目の ID と、新しいデータ値。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_WMI\_インスタンス\_いない\_が見つかりました

ステータス\_WMI\_ITEMID\_いない\_が見つかりました

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_WMI\_読み取り\_のみ

ステータス\_WMI\_設定\_エラー

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、ドライバーが、ルーチンを呼び出す[ *DpWmiSetDataItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)ルーチン、またはステータスを返します\_WMI\_読み取り\_ドライバーは、ルーチンを定義していない場合のみです。

ドライバーが処理する場合**IRP\_MN\_変更\_単一\_項目**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**指すドライバーに渡されたポインターと同じデバイス オブジェクト[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

サポートを実装しない**IRP\_MN\_変更\_単一\_項目**システム提供のユーザー モード コンポーネントがこの機能が必要であることを確認する場合を除いて、します。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない場合ドライバーする必要があります IRP が失敗して、状態を返す\_WMI\_GUID\_いない\_が見つかりました。

入力を確認する必要があります、ドライバーは、データ ブロックをサポートする場合[**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)構造体**Parameters.WMI.Buffer**インスタンス名に対応、としては、次のようにする点します。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_で名前が設定されて**WnodeHeader.Flags**、ドライバーを使用して**InstanceIndex**へのインデックスとして、そのブロックの静的インスタンス名のドライバーの一覧。 WMI では、ブロックが登録されているときに、ドライバーによって提供される登録データからインデックスを取得します。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_名が明確では**WnodeHeader.Flags、** ドライバーは、オフセットを使用して**OffsetInstanceName**に入力内でインスタンス名の文字列を検索[**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)構造体。 **OffsetInstanceName** USHORT サイズの長さをバイト (文字ではなく) でインスタンス名の文字列の構造体の先頭からのバイト オフセットです。 この長さが含まれています、終端 NULL には場合、現時点では、その後にインスタンス名の文字列を Unicode で。

ドライバーがすべての入力値を検証する責任を負います。 具体的には、ドライバーは IRP 要求自体を処理する場合、次を実行する必要があります。

-   静的な名前のことを確認します、 **InstanceIndex** 、れた WNODE のメンバー\_単一\_データ ブロックのドライバーでサポートされているインスタンスのインデックスの範囲内の項目の構造は。

-   動的な名前は、インスタンス名の文字列が、ドライバーでサポートされるデータ ブロックのインスタンスを識別することを確認します。

-   いることを確認、 **ItemId**のメンバー、 [**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)でサポートされている項目の識別子の範囲内の構造は、データ ブロックのドライバーです。

-   いることを確認、 **DataBlockOffset**と**SizeDataItem**のメンバー、**れた WNODE\_単一\_項目**構造体が有効なサイズのデータについて説明しますブロックとバッファーの内容がデータ項目に対して無効です。

-   指定されたデータ項目が 1 つのドライバーを呼び出し元によって開始された変更が可能であることを確認します。 つまり、ドライバーは読み取り専用にしようとしたデータ項目に対する変更を許可しないでください。

発信側ユーザー モード アプリケーションのスレッド コンテキストと見なさないでください: より高度なドライバー、変更がある可能性があります。

ドライバーでは、指定されたインスタンスで特定できない場合は、IRP が失敗し、状態を返すする必要があります\_WMI\_インスタンス\_いない\_が見つかりました。 動的なインスタンスの名前を持つインスタンスの場合は、この状態は、ドライバーが、インスタンスをサポートしていないことを示します。 WMI は、他のデータ プロバイダーのクエリを実行し、別のプロバイダーはインスタンスを検索しますが、何らかの理由で要求を処理できない場合は、適切なエラーをデータ コンシューマーに返されます。 そのため続行できます。

データ項目の値にインスタンスの場合は、ドライバーは、インスタンスを検索し、要求を処理できる、設定、 [**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)します。 データ項目が読み取り専用の場合は、ドライバーが項目変更せずに、失敗、IRP のままし、ステータスを返します\_WMI\_読み取り\_のみです。

インスタンスが有効では、ドライバーが要求を処理できない場合は、すべての該当するエラー状態を返すできます。

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


[*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**れた WNODE\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)

 

 




