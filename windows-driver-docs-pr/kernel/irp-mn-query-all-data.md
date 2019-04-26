---
title: IRP_MN_QUERY_ALL_DATA
description: WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 5a3caa66f4b6b68b32f7fd712619b76492cf73f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342705"
---
# <a name="irpmnqueryalldata"></a>IRP\_MN\_クエリ\_すべて\_データ


WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)処理するために、 **IRP\_MN\_クエリ\_すべて\_データ**で WMI を要求します。有効にする呼び出しのドライバーの[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、指定されたデータ ブロックのすべてのインスタンスのクエリをこの IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId** IRP がドライバーの I/O スタックの場所には、要求に応答する必要がありますドライバーのデバイス オブジェクトを指しています。

**Parameters.WMI.DataPath**データ ブロックを識別する GUID を指します。

**Parameters.WMI.BufferSize** nonpaged、バッファーの最大サイズを示す**Parameters.WMI.Buffer**、要求からの出力データを受信します。 バッファー サイズが以上にする必要があります**sizeof**(**れた WNODE\_すべて\_データ**) さらに、インスタンスの名前と返されるすべてのインスタンスのデータのサイズ。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI を入力、**れた WNODE\_すべて\_データ**呼び出してドライバーの*DpWmiQueryDataBlock*ドライバーによって登録された各ブロックに対して 1 回ルーチン。

それ以外の場合、ドライバーを設定、 [**れた WNODE\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff566372)で構造体**Parameters.WMI.Buffer**次のようにします。

-   設定**WnodeHeader.BufferSize**全体のバイト数に**れた WNODE\_すべて\_データ**返され、次のように設定します**WnodeHeader.Timestamp**。によって返される値**KeQuerySystemTime**、設定と**WnodeHeader.Flags**必要に応じて、返されるデータにします。

-   セット**InstanceCount**返されるインスタンスの数。

-   ブロックは、動的なインスタンス名を使用している場合は、設定**OffsetInstanceNameOffsets** (バイト単位) の先頭からのオフセットを**れた WNODE\_すべて\_データ**先 ULONG の配列オフセットを開始します。 この配列内の各要素からのオフセット、**れた WNODE\_すべて\_データ**各動的インスタンス名が格納されています。 各動的インスタンス名は、数が、Unicode 文字列を続けて USHORT がカウントされた Unicode 文字列として格納されます。 カウントでは、Unicode 文字列の一部には、終端の null 文字は含まれません。 この null 文字に設定されているサイズ内に収める必要がありますも Unicode 文字列には、終端の null 文字が含まれますが場合、 **WNodeHeader.BufferSize**します。

-   すべてのインスタンスが同じサイズの場合。
    -   れた WNODE を設定\_フラグ\_固定\_インスタンス\_サイズ**WnodeHeader.Flags**設定と**FixedInstanceSize** (バイト単位)、そのサイズにします。
    -   開始位置として、インスタンス データを書き込む**DataBlockOffset**、パディングの各インスタンスは、8 バイト境界に一致するようにします。 たとえば場合、 **FixedInstanceSize** 6 は、ドライバーが 2 バイトのインスタンス間の余白を追加します。
-   インスタンスは、サイズに変化する場合。
    -   クリアれた WNODE\_フラグ\_固定\_インスタンス\_サイズ**WnodeHeader.Flags**の配列を書き込みます**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**構造体の開始位置として**OffsetInstanceDataAndLength**します。 各**OFFSETINSTANCEDATAANDLENGTH**構造体の先頭からのバイト オフセットを指定します、**れた WNODE\_すべて\_データ**ごとに、データの先頭に構造体インスタンス、およびデータの長さ。 **DataBlockOffset**は使用されません。

    -   最後の要素の後にインスタンス データを書き込み、 **OffsetInstanceDataAndLength**配列、および各インスタンスは、8 バイト境界に一致するようにパディングします。

場合、バッファー **Parameters.WMI.Buffer**が小さすぎるで必要なサイズを設定、ドライバーのすべてのデータを受信する、 [**れた WNODE\_すぎます\_小さな**](https://msdn.microsoft.com/library/windows/hardware/ff566379)で構造体**Parameters.WMI.Buffer**します。 バッファーがより小さい場合**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーは IRP が失敗し、ステータスを返します\_バッファー\_すぎます\_小さい。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_バッファー\_すぎます\_小さな

ステータス\_WMI\_GUID\_いない\_が見つかりました

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information** 、バッファーに書き込まれたバイト数に**Parameters.WMI.Buffer**します。

<a name="operation"></a>操作
---------

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーが、ルーチンを呼び出す[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチン。

ドライバーが処理する場合、 **IRP\_MN\_クエリ\_すべて\_データ**要求と、その方がよい場合にのみ**Parameters.WMI.ProviderId**指す同じドライバーに渡されるデバイス オブジェクト[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

ドライバーは、データ ブロックをサポートする場合、次の操作する必要があります。

-   いることを確認**Parameters.WMI.BufferSize**ドライバーから返されるすべてのデータを受信するのに十分な大きさであるバッファーを指定します。

-   入力、 [**れた WNODE\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff566372)で構造体**Parameters.WMI.Buffer**にそのデータ ブロックのすべてのインスタンス データ。

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


[*DpWmiQueryDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544096)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**KeQuerySystemTime**](https://msdn.microsoft.com/library/windows/hardware/ff553068)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**れた WNODE\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff566372)

 

 




