---
title: IRP_MJ_PNP
description: IRP\_MJ\_PNP
ms.assetid: aec2f309-02a1-460a-b674-33ad18286347
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_PNP
topic_type:
- apiref
api_name:
- IRP_MJ_PNP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 064ef8319c3e9fe9cf48a54277f8444113baa903
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852256"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


## <a name="when-sent"></a>送信時


プラグアンドプレイ Manager は、 \_ \_ システムでプラグアンドプレイアクティビティが発生するたびに、IRP MJ PNP 要求を送信します。 その他のオペレーティングシステムコンポーネントおよびその他のカーネルモードドライバーは、 \_ \_ マイナー関数コードに応じて、特定の IRP MJ PNP 要求を送信することもできます。

ドライバーのプラグアンドプレイの IRP 処理要件の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

IRP MJ PNP のマイナー関数コードに関する参照情報について \_ \_ は、「[プラグアンドプレイの小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)」を参照してください。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムは、マイナー関数のコードを確認して、どの操作が要求されているかを判断する必要があります。 ファイルシステムでは、次のマイナー関数コードを処理する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_CANCEL_REMOVE_DEVICE</p></td>
<td align="left"><p>以前のクエリ削除要求が取り消されたことを示します。 この要求は、キャンセルに関連するクリーンアップを実行する必要がある場合に、ファイルシステムに警告するために送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>デバイスが削除されようとしていることを示します。 ファイルシステムがデバイスにマウントされている場合、PnP マネージャーはこの要求をファイルシステムとファイルシステムフィルターに送信します。 デバイスに開いているハンドルがある場合、通常、ファイルシステムはクエリ削除要求に失敗します。 それ以外の場合、通常、ファイルシステムはボリュームをロックして、今後の作成要求が成功しないようにします。 マウントされたファイルシステムがクエリ削除要求をサポートしていない場合、PnP マネージャーはデバイスのクエリ削除要求に失敗します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>デバイスが削除されようとしていることを示します。 ファイルシステムがデバイスにマウントされている場合、PnP マネージャーは、この IRP をファイルシステムとファイルシステムフィルターに送信します。 ファイルシステムは、この IRP をデバイスのストレージドライバーにすぐに渡す必要があります。その後、ファイルシステムによってボリュームがマウント解除される完了ルーチンを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>デバイスが起動中であることを示します。 ファイルシステムは、この IRP をデバイスのストレージドライバーに渡す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>デバイスが削除されたことを示します。 ファイルシステムがデバイスにマウントされている場合、PnP マネージャーは、この IRP をファイルシステムとファイルシステムフィルターに送信します。 ファイルシステムは、この IRP をデバイスのストレージドライバーにすぐに渡す必要があります。その後、ファイルシステムによってボリュームがマウント解除される完了ルーチンを設定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ファイルシステムフィルタードライバーは、次のガイドラインに従って、PnP Irp を処理する必要があります。

-   ユーザーがボリュームを正常に削除しようとすると、PnP マネージャーは、IRP を使用した \_ \_ クエリの \_ 削除デバイス要求を送信し \_ ます。 この IRP を受信すると、フィルターはボリューム上の開いているハンドルをすべて閉じ、スタック上の次の下位のドライバーに IRP を渡します。 これは非常に重要です。 ドライバーが開いているハンドルをすべて閉じるのに失敗した場合、ボリュームがマウント解除されないようにします。これにより、物理デバイスの取り出しを防止できます。

> [!NOTE]
> IRP は、 \_ デバイスの \_ 削除要求を受信すると \_ \_ 、安全に削除できるすべてのボリュームを直ちにマウント解除します。 そのため、FAT ボリュームにアタッチされたフィルターは、フィルターの完了ルーチンが呼び出される前に、そのフィルターデバイスオブジェクトが解放されることを期待する必要があります。 NTFS ファイルシステムでは、この操作は行われません。 そのため、NTFS ボリュームにアタッチされたフィルターは、フィルターの完了ルーチンが呼び出されたときに、そのデバイスオブジェクトがボリュームにアタッチされることを期待できます。

     

-   Irp が完了した後に受信される irp はデバイス要求を削除しますが、IRP によって削除されたデバイスの削除要求または IRP の削除後のデバイス要求を受信 \_ \_ \_ \_ する前に \_ \_ \_ \_ \_ \_ \_ 、スタックを (ストレージデバイススタックによって失敗するように) 安全に渡すことができます。

-   IRP による \_ \_ クエリの \_ \_ 削除要求に応じて、ボリュームの開いているハンドルをすべて既に閉じた後に、フィルターが irp を完了したデバイスの削除要求を受け取る \_ \_ \_ \_ と、ハンドルを再び開くことができます。 ただし、フィルターは、IRP がスタック内のドライバーによって正常に完了した後で、完了ルーチンでのみ実行できます。

-   フィルターは、irp が完了したデバイスの削除要求を受信したときに、irp で irp を保持していない \_ \_ \_ 限り、irp で処理を実行する必要はありません \_ \_ \_ \_ 。 キューで Irp を保持している場合、フィルターはそのボリュームのすべての Irp をデキューし、エラーが発生した &lt; &gt; 後、 &lt; &gt; スタック上の次の下位のドライバーに irp を渡す前に失敗します。

-   IRP の突然の \_ \_ \_ 削除要求を受信すると、フィルターは次の操作を実行します。

    -   未処理の参照がないまでファイルシステムがスタックをクリーンアップできないため、開いているすべてのハンドルをボリュームに対して閉じます。

    -   フィルターが Irp をキューに保持している場合は、エラーを発生させるか、スタックに渡すことができます (ストレージデバイススタックによって失敗する場合)。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、プラグアンドプレイ要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
PnP Irp の場合、このポインターは**NULL**である必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP MJ PNP を指定し \_ \_ ます。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; minorfunction*  
次のいずれかです。

-   IRP を終了する \_ \_ \_ デバイスの削除 \_
-   IRP を実行する \_ \_ クエリ \_ デバイスの削除 \_
-   IRP のすべての \_ \_ デバイスの削除 \_
-   IRP の全 \_ \_ 開始 \_ デバイス
-   IRP \_ の \_ 突然の \_ 削除

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ PNP (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP を終了する \_ \_ \_ デバイスの削除 \_**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)

[**IRP を実行する \_ \_ クエリ \_ デバイスの削除 \_**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP のすべての \_ \_ デバイスの削除 \_**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP の全 \_ \_ 開始 \_ デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP \_ の \_ 突然の \_ 削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

 

 






