---
title: IRP_MJ_WRITE
description: システムからデバイスにデータを転送するすべてのデバイスドライバーは、DispatchWrite または DispatchReadWrite のルーチンで書き込み要求を処理する必要があります。これは、このようなデバイスドライバーの上層にある上位レベルのドライバーである必要があります。
ms.date: 08/12/2017
ms.assetid: d0db505e-2b3c-4b69-83ef-1a52e37e5d1a
keywords:
- IRP_MJ_WRITE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 134a755caefff7d64ab387a9c6d184092896bfb2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838593"
---
# <a name="irp_mj_write"></a>IRP\_MJ\_WRITE


システムからデバイスにデータを転送するすべてのデバイスドライバーは、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)または[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)のルーチンで書き込み要求を処理する必要があります。これは、このようなデバイスドライバーの上層にある上位レベルのドライバーである必要があります。

<a name="when-sent"></a>送信時
---------

作成要求が正常に完了した後、いつでも実行できます。

場合によっては、ターゲットデバイスオブジェクトを表すファイルオブジェクトのハンドルを持つユーザーモードアプリケーションまたは Win32 コンポーネントが、デバイスへのデータ転送を要求している可能性があります。 場合によっては、上位レベルのドライバーが書き込み IRP を作成および設定している可能性があります。

## <a name="input-parameters"></a>入力パラメーター


IRP 内のドライバーの i/o スタックの場所は、パラメーターで転送するバイト数を示します。**長さ**。

一部のドライバーでは、**パラメーター**に値を使用しています。キーを使用して、受信書き込み要求を、デバイスキュー内、またはドライバーによって管理される irp の内部キューで並べ替えます。

特定の種類のドライバーでは、パラメーターにも値が使用されます。書き込みは、転送操作の開始オフセットを示します **。** 例については、「インストール可能ファイルシステム (IFS)」ドキュメントの「 [**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write) 」を参照してください。

基になるデバイスドライバによってターゲットデバイスオブジェクトの**フラグ**が設定されているかどうかによって\_IO\_io または\_ダイレクト\_io によって、次のいずれかからデータが転送されます。

-   ドライバーがバッファーされた i/o を使用する場合は、 **Irp-&gt;AssociatedIrp**のバッファー

-   基になるデバイスドライバーが直接 i/o (DMA または PIO) を使用している場合、Irp で記述されているバッファー ( **Irp-&gt;MdlAddress**)

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

書き込み要求の受信時に、上位レベルのドライバーは、次の下位のドライバーの i/o スタックの場所を IRP 内に設定します。または、1つまたは複数の下位のドライバーに対して追加の Irp を作成および設定します。 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すことによって、入力 irp に対しては省略可能で、ドライバーで作成された irp に必要な[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できます。 次に、ドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、要求を次の下位のドライバーに渡します。

書き込み要求を受信すると、デバイスドライバーはシステムメモリからデバイスにデータを転送します。 デバイスドライバーは、i/o 状態ブロックの**情報**フィールドを、IRP の完了時に転送されたバイト数に設定します。

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


[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)

[**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)

 

 




