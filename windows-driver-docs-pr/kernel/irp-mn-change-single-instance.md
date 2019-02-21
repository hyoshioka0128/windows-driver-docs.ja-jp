---
title: IRP_MN_CHANGE_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 180d40a4-b300-4801-b9da-9239500ca15f
keywords:
- IRP_MN_CHANGE_SINGLE_INSTANCE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 20b9afcc67cf6b42a31b54c4be11988ab9cb121d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531274"
---
# <a name="irpmnchangesingleinstance"></a>IRP\_MN\_変更\_単一\_インスタンス


WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)処理するために、 **IRP\_MN\_変更\_単一\_インスタンス**要求と、WMI を呼び出してドライバーの[ *DpWmiSetDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544104)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、データ ブロックの 1 つのインスタンス内のすべてのデータ項目を変更するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターには、ドライバーの IRP で I/O スタックの場所が記載されています。

**Parameters.WMI.DataPath**変更するインスタンスに関連付けられているデータ ブロックを識別する GUID をポイントします。

**Parameters.WMI.BufferSize** nonpaged、バッファーのサイズを示します**Parameters.WMI.Buffer**します。

**Parameters.WMI.Buffer**を指す、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)構造体のインスタンスを識別し、新しいデータ値を指定します。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_WMI\_インスタンス\_いない\_が見つかりました

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_WMI\_読み取り\_のみ

ステータス\_WMI\_設定\_エラー

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーが、ルーチンを呼び出す[ *DpWmiSetDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544104)ルーチン、またはステータスを返します\_WMI\_読み取り\_ドライバーは、ルーチンを定義していない場合のみです。

ドライバーが処理する場合、 **IRP\_MN\_変更\_単一\_インスタンス**自体、要求は、デバイス オブジェクトのポインターにする場合にのみ**Parameters.WMI.ProviderId**呼び出しで、ドライバーによって渡されたポインターと一致する[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

GUID をまず確認する必要があります、ドライバーは、要求を処理する場合**Parameters.WMI.DataPath**ドライバーでサポートされるデータ ブロックを識別するかどうかを判断します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

受信した確認する必要がありますが、ドライバーは、データ ブロックをサポートする場合[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)で構造体**Parameters.WMI.Buffer**の次のように、インスタンス名。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_で名前が設定されて**WnodeHeader.Flags**、ドライバーを使用して**InstanceIndex**へのインデックスとして、そのブロックの静的インスタンス名のドライバーの一覧。 WMI では、ブロックが登録されているときに、ドライバーによって提供される登録データからインデックスを取得します。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_名が明確では**WnodeHeader.Flags、** ドライバーは、オフセットを使用して**OffsetInstanceName**に入力内でインスタンス名の文字列を検索[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)します。 **OffsetInstanceName** unicode 形式でインスタンス名の文字列で後に存在する場合は、終端の null を含む USHORT サイズの長さをバイト (しない文字) でインスタンス名の文字列の構造体の先頭からのバイト オフセット。

ドライバーがすべての入力値を検証する責任を負います。 具体的には、ドライバーは IRP 要求自体を処理する場合、次を実行する必要があります。

-   静的の名のことを確認します、 **InstanceIndex**のメンバー、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)がの範囲内に構造体インスタンスのデータ ブロックのドライバーでサポートされるインデックス。

-   動的な名前は、インスタンス名の文字列が、ドライバーでサポートされるデータ ブロックのインスタンスを識別することを確認します。

-   いることを確認、 **DataBlockOffset**と**SizeDataBlock**のメンバー、**れた WNODE\_単一\_インスタンス**構造体は、有効なサイズについて説明します項目、データの間存在して、バッファーの内容は、データ ブロックに対して有効な埋め込みのデータ ブロック。

-   指定されたデータ ブロックが、ドライバーにより、呼び出し元によって開始された変更を 1 つであることを確認します。 つまり、ドライバーは読み取り専用にしようとしたデータ ブロックに対する変更を許可しないでください。

発信側ユーザー モード アプリケーションのスレッド コンテキストと見なさないでください: より高度なドライバー、変更がある可能性があります。

ドライバーでは、指定されたインスタンスで特定できない場合は、IRP が失敗し、状態を返すする必要があります\_WMI\_インスタンス\_いない\_が見つかりました。 インスタンスに動的なインスタンス名がある場合は、この状態は、ドライバーが、インスタンスをサポートしていないことを示します。 WMI は、他のデータ プロバイダーのクエリを実行し、別のプロバイダーはインスタンスを検索しますが、何らかの理由で要求を処理できない場合は、適切なエラーをデータ コンシューマーに返されます。 そのため続行できます。

ドライバーは、インスタンスを検索し、要求を処理できる場合、内の値のインスタンスで、書き込み可能なデータ項目は設定、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)構造体読み取り専用項目は変更されません。 ドライバーが IRP を失敗し、状態を返すデータ ブロック全体が読み取り専用の場合は、\_WMI\_読み取り\_のみです。

インスタンスが有効では、ドライバーが要求を処理できない場合は、すべての該当するエラー状態を返すできます。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DpWmiSetDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544104)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)

 

 




