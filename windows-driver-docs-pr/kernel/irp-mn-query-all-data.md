---
title: IRP_MN_QUERY_ALL_DATA
description: WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 4d6dd8105b4d3c878ad87f0765d4281ca24a102f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383295"
---
# <a name="irpmnqueryalldata"></a>IRP\_MN\_クエリ\_すべて\_データ


WMI をサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)処理するために、 **IRP\_MN\_クエリ\_すべて\_データ**で WMI を要求します。有効にする呼び出しのドライバーの[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)ルーチン。

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


ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI を入力、**れた WNODE\_すべて\_データ**呼び出してドライバーの*DpWmiQueryDataBlock*ドライバーによって登録された各ブロックに対して 1 回ルーチン。

それ以外の場合、ドライバーを設定、 [**れた WNODE\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)で構造体**Parameters.WMI.Buffer**次のようにします。

-   設定**WnodeHeader.BufferSize**全体のバイト数に**れた WNODE\_すべて\_データ**返され、次のように設定します**WnodeHeader.Timestamp**。によって返される値**KeQuerySystemTime**、設定と**WnodeHeader.Flags**必要に応じて、返されるデータにします。

-   セット**InstanceCount**返されるインスタンスの数。

-   ブロックは、動的なインスタンス名を使用している場合は、設定**OffsetInstanceNameOffsets** (バイト単位) の先頭からのオフセットを**れた WNODE\_すべて\_データ**先 ULONG の配列オフセットを開始します。 この配列内の各要素からのオフセット、**れた WNODE\_すべて\_データ**各動的インスタンス名が格納されています。 各動的インスタンス名は、数が、Unicode 文字列を続けて USHORT がカウントされた Unicode 文字列として格納されます。 カウントでは、Unicode 文字列の一部には、終端の null 文字は含まれません。 この null 文字に設定されているサイズ内に収める必要がありますも Unicode 文字列には、終端の null 文字が含まれますが場合、 **WNodeHeader.BufferSize**します。

-   すべてのインスタンスが同じサイズの場合。
    -   れた WNODE を設定\_フラグ\_固定\_インスタンス\_サイズ**WnodeHeader.Flags**設定と**FixedInstanceSize** (バイト単位)、そのサイズにします。
    -   開始位置として、インスタンス データを書き込む**DataBlockOffset**、パディングの各インスタンスは、8 バイト境界に一致するようにします。 たとえば場合、 **FixedInstanceSize** 6 は、ドライバーが 2 バイトのインスタンス間の余白を追加します。
-   インスタンスは、サイズに変化する場合。
    -   クリアれた WNODE\_フラグ\_固定\_インスタンス\_サイズ**WnodeHeader.Flags**の配列を書き込みます**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**構造体の開始位置として**OffsetInstanceDataAndLength**します。 各**OFFSETINSTANCEDATAANDLENGTH**構造体の先頭からのバイト オフセットを指定します、**れた WNODE\_すべて\_データ**ごとに、データの先頭に構造体インスタンス、およびデータの長さ。 **DataBlockOffset**は使用されません。

    -   最後の要素の後にインスタンス データを書き込み、 **OffsetInstanceDataAndLength**配列、および各インスタンスは、8 バイト境界に一致するようにパディングします。

場合、バッファー **Parameters.WMI.Buffer**が小さすぎるで必要なサイズを設定、ドライバーのすべてのデータを受信する、 [**れた WNODE\_すぎます\_小さな**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)で構造体**Parameters.WMI.Buffer**します。 バッファーがより小さい場合**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーは IRP が失敗し、ステータスを返します\_バッファー\_すぎます\_小さい。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_バッファー\_すぎます\_小さな

ステータス\_WMI\_GUID\_いない\_が見つかりました

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information** 、バッファーに書き込まれたバイト数に**Parameters.WMI.Buffer**します。

<a name="operation"></a>操作
---------

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、ドライバーが、ルーチンを呼び出す[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)ルーチン。

ドライバーが処理する場合、 **IRP\_MN\_クエリ\_すべて\_データ**要求と、その方がよい場合にのみ**Parameters.WMI.ProviderId**指す同じドライバーに渡されるデバイス オブジェクト[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

ドライバーは、データ ブロックをサポートする場合、次の操作する必要があります。

-   いることを確認**Parameters.WMI.BufferSize**ドライバーから返されるすべてのデータを受信するのに十分な大きさであるバッファーを指定します。

-   入力、 [**れた WNODE\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)で構造体**Parameters.WMI.Buffer**にそのデータ ブロックのすべてのインスタンス データ。

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


[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**れた WNODE\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)

 

 




