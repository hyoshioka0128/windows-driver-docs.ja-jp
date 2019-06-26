---
title: IRP_MJ_READ
description: システムにそのデバイスからデータを転送するすべてのデバイス ドライバーには、このようなデバイス ドライバーの上層により高度なドライバーをする必要があります、DispatchRead または DispatchReadWrite ルーチン内の読み取り要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5ae4c6c5-d8f2-4dc5-8cfd-ecb751fc88be
keywords:
- IRP_MJ_READ カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 0be7c5512778f006f6399b747b14558095a66cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370898"
---
# <a name="irpmjread"></a>IRP\_MJ\_READ


システムにそのデバイスからデータを転送するすべてのデバイス ドライバーでの読み取り要求を処理する必要があります、 [ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)としてする必要があります、日常的な高度なドライバーの上層にこのようなデバイス ドライバー。

<a name="when-sent"></a>送信時
---------

いつの作成要求が正常に完了します。

場合によっては、ユーザー モード アプリケーションまたはターゲット デバイス オブジェクトを表すファイル オブジェクトのハンドルを持つ Win32 コンポーネントは、デバイスからのデータ転送を要求が。 場合によってより高度なドライバーが作成され、読み取り IRP を設定します。

## <a name="input-parameters"></a>入力パラメーター


IRP のドライバーの I/O スタックの場所に転送するバイト数を示す**Parameters.Read.Length**します。

一部のドライバーにある値を使用して、 **Parameters.Read.Key**デバイスのキューまたは Irp のドライバー管理の内部キューでは、ドライバーにより決定された順序に受信した読み取り要求を分類します。

ドライバーの特定の種類がある値を使用しても**Parameters.Read.ByteOffset**、転送操作の開始オフセットを示します。 たとえばを参照してください、 [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)インストール可能なファイル システム (IFS) ドキュメントのトピックです。

## <a name="output-parameters"></a>出力パラメーター


ターゲット デバイス オブジェクトの基になるデバイス ドライバーを設定するかどうかに応じて**フラグ**か\_バッファーに格納された\_IO またはで\_直接\_のいずれかに IO、データが転送されます。次:

-   バッファー **Irp -&gt;AssociatedIrp.SystemBuffer**ドライバーがバッファー内の I/O を使用している場合。

-   MDL で説明されているバッファー **Irp -&gt;MdlAddress**基になるデバイス ドライバーがダイレクト I/O (DMA または PIO) を使用している場合。

<a name="operation"></a>操作
---------

読み取り要求の受信後より高度なドライバーは、次の下位ドライバー用の IRP で I/O スタックの場所を設定または作成し、1 つまたは複数の下位のドライバーの追加の Irp を設定します。 これを設定することができます、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、日常的なは入力 IRP の省略可能ですが Irp のドライバーが作成に必要な呼び出して[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine). 次に、ドライバーが要求を使用してドライバーを次の下位を渡します[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

読み取り要求の受信後は、デバイス ドライバーは、システム メモリをそのデバイスからデータを転送します。 デバイス ドライバーのセット、**情報**IRP の完了時に I/O 状態ブロックのバイト数のフィールドが転送されます。

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


[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)

 

 




