---
title: IRP_MJ_READ
description: デバイスからシステムにデータを転送するすべてのデバイスドライバーは、DispatchRead または DispatchReadWrite のルーチンで読み取り要求を処理する必要があります。これは、そのようなデバイスドライバーの上層にある上位レベルのドライバーである必要があるためです。
ms.date: 08/12/2017
ms.assetid: 5ae4c6c5-d8f2-4dc5-8cfd-ecb751fc88be
keywords:
- IRP_MJ_READ カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 5d001bb0c37ece3a55b09ccda0e283db670e3060
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838600"
---
# <a name="irp_mj_read"></a>IRP\_MJ\_READ


デバイスからシステムにデータを転送するすべてのデバイスドライバーは、 [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)のルーチンで読み取り要求を処理する必要があります。これは、そのようなデバイスドライバーの上層にある上位レベルのドライバーである必要があるためです。

<a name="when-sent"></a>送信時
---------

作成要求が正常に完了した後、いつでも実行できます。

場合によっては、ターゲットデバイスオブジェクトを表すファイルオブジェクトのハンドルを持つユーザーモードアプリケーションまたは Win32 コンポーネントが、デバイスからのデータ転送を要求している可能性があります。 場合によっては、上位レベルのドライバーで読み取り IRP が作成され、設定されている可能性があります。

## <a name="input-parameters"></a>入力パラメーター


IRP 内のドライバーの i/o スタックの場所は、パラメーターで転送するバイト数を示します。 **Length**.

一部のドライバーでは、**パラメーター**に値を使用しています。キーは、デバイスキューまたはドライバーによって管理される irp の内部キューで、受信した読み取り要求をドライバーによって決まる順序に並べ替えるために使用します。

特定の種類のドライバーでは、パラメーターにも値が使用さ**れます。 Read. ByteOffset**は、転送操作の開始オフセットを示します。 例については、「インストール可能ファイルシステム (IFS)」ドキュメントの「 [**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read) 」を参照してください。

## <a name="output-parameters"></a>出力パラメーター


基になるデバイスドライバによってターゲットデバイスオブジェクトの**フラグ**が設定されているかどうかによって\_IO\_io または\_DIRECT\_io によって、次のいずれかにデータが転送されます。

-   ドライバーがバッファーされた i/o を使用する場合は、 **Irp-&gt;AssociatedIrp**のバッファー。

-   基になるデバイスドライバーが直接 i/o (DMA または PIO) を使用している場合は、MDL によって記述された、Irp で記述されたバッファー **&gt;MdlAddress** 。

<a name="operation"></a>操作
---------

上位レベルのドライバーは、読み取り要求の受信時に、次に低いドライバーの IRP 内の i/o スタックの場所を設定します。または、1つまたは複数の下位のドライバーに対して追加の Irp を作成および設定します。 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すことによって、入力 irp に対しては省略可能で、ドライバーで作成された irp に必要な[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できます。 次に、ドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、要求を次の下位のドライバーに渡します。

デバイスドライバーは、読み取り要求の受信時に、デバイスからシステムメモリにデータを転送します。 デバイスドライバーは、i/o 状態ブロックの**情報**フィールドを、IRP の完了時に転送されたバイト数に設定します。

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


[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)

 

 




