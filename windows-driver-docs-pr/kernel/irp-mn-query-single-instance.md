---
title: IRP_MN_QUERY_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 104b6b3e-aa5d-437f-8236-02e4abb1ba46
keywords:
- IRP_MN_QUERY_SINGLE_INSTANCE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: dfaea0793f295343a527b2f9f00f2fe7976eadaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381414"
---
# <a name="irpmnquerysingleinstance"></a>IRP\_MN\_クエリ\_単一\_インスタンス


WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)処理するために、 **IRP\_MN\_クエリ\_単一\_インスタンス**要求と、WMI を呼び出してドライバーの[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、指定されたデータ ブロックの 1 つのインスタンスのクエリをこの IRP を送信します。

WMI の送信、 **IRP\_MN\_クエリ\_単一\_インスタンス**送信する前に、 [ **IRP\_MN\_EXECUTE\_メソッド**](irp-mn-execute-method.md)します。 ドライバーをサポートしている場合**IRP\_MN\_EXECUTE\_メソッド**、必要があります、 **IRP\_MN\_クエリ\_単一\_インスタンス**メソッドが実行されている同じデータ ブロックのハンドラー。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**をクエリするデータ ブロックを識別する GUID を指します。

**Parameters.WMI.BufferSize** nonpaged、バッファーの最大サイズを示す**Parameters.WMI.Buffer**を[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)クエリ インスタンスを識別する構造体。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI を入力、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)ドライバーのによって提供されるデータの構造体[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチン。

それ以外の場合、ドライバーの設定、**れた WNODE\_単一\_インスタンス**で構造体**Parameters.WMI.Buffer**次のように。

-   更新プログラム**WnodeHeader.BufferSize**出力のバイト単位のサイズ、**れた WNODE\_単一\_インスタンス**インスタンス データを含む構造。 この値は (インスタンス データのクアッド ワード境界で開始されるようにパディングされる) インスタンス名の長さを含める必要があります、クエリ対象のクラスが静的登録されている場合でもインスタンス名およびドライバー開発者はいない明示的に名前を指定して処理するときにこの IRP します。

-   セット**SizeDataBlock**インスタンス データのバイト単位のサイズにします。 静的なインスタンス名を使用している場合、この値は、インスタンス名のサイズを含めないでください。

-   インスタンス データを書き込みます**Parameters.WMI.Buffer**開始位置として**DataBlockOffset**します。 ドライバーは、入力値を変更する必要があります**DataBlockOffset**します。

場合、バッファー **Parameters.WMI.Buffer**が小さすぎてすべてに必要なサイズでドライバーの塗りつぶし、データの受信を[**れた WNODE\_すぎます\_小さな**](https://msdn.microsoft.com/library/windows/hardware/ff566379)で構造体**Parameters.WMI.Buffer**します。 バッファーがより小さい場合**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーは IRP が失敗し、ステータスを返します\_バッファー\_すぎます\_小さい。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_バッファー\_すぎます\_小さな

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_WMI\_インスタンス\_いない\_が見つかりました

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**に入力された値に**WnodeHeader.BufferSize**します。 この値には、静的なインスタンス名の長さが含まれています。

<a name="operation"></a>操作
---------

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、 **WmiSystemControl**呼び出してドライバーの[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチン。

ドライバーが処理する場合、 **IRP\_MN\_クエリ\_単一\_インスタンス**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**ドライバーの呼び出しで渡されたポインターと同じデバイス オブジェクトを指し示す[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、デバイス スタックの次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

ドライバーがすべての入力値を検証する責任を負います。 具体的には、ドライバーは IRP 要求自体を処理する場合、次を実行する必要があります。

-   静的の名のことを確認します、 **InstanceIndex**のメンバー、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)がの範囲内に構造体インスタンスのデータ ブロックのドライバーでサポートされるインデックス。

-   動的な名前は、インスタンス名の文字列が、ドライバーでサポートされるデータ ブロックのインスタンスを識別することを確認します。

-   いることを確認**Parameters.WMI.BufferSize**ドライバーから返されるすべてのデータを受信するのに十分な大きさであるバッファーを指定します。

ドライバーは、データ ブロックをサポートする場合、入力を確認します[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)で**Parameters.WMI.Buffer**インスタンス。名前としては、次のようにします。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_で名前が設定されて**WnodeHeader.Flags**、ドライバーを使用して**InstanceIndex**へのインデックスとして、そのブロックの静的インスタンス名のドライバーの一覧。 WMI では、ブロックが登録されているときに、ドライバーによって提供される登録データからインデックスを取得します。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_名が明確では**WnodeHeader.Flags**、ドライバーは、オフセットを使用して**OffsetInstanceName**に入力内でインスタンス名の文字列を検索**れた WNODE\_単一\_インスタンス**します。 **OffsetInstanceName**でインスタンス名の文字列で後に存在する場合は、終端の null を含むバイト (しない文字) でインスタンス名文字列の長さである、USHORT、構造体の先頭からのバイト単位のオフセットUnicode。

ドライバーでは、指定されたインスタンスで特定できない場合は、IRP が失敗し、状態を返すする必要があります\_WMI\_インスタンス\_いない\_が見つかりました。 動的なインスタンスの名前を持つインスタンスの場合は、この状態は、ドライバーが、インスタンスをサポートしていないことを示します。 WMI は、他のデータ プロバイダーのクエリを実行し、別のプロバイダーはインスタンスを検索しますが、何らかの理由で要求を処理できない場合は、適切なエラーをデータ コンシューマーに返されます。 そのため続行できます。

塗りつぶす場合は、ドライバーは、インスタンスを検索し、要求を処理できる、**れた WNODE\_単一\_インスタンス**で構造体**Parameters.WMI.Buffer**インスタンスのデータ。

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


[*DpWmiQueryDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544096)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)

 

 




