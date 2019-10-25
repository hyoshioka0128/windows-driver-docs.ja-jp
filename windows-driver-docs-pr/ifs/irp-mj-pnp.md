---
title: IRP_MJ_PNP
description: IRP\_MJ\_PNP
ms.assetid: aec2f309-02a1-460a-b674-33ad18286347
keywords:
- IRP_MJ_PNP インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_PNP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca7a088ebcade4b4211e39b8dd349bbf36c5cfc4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841170"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


## <a name="when-sent"></a>送信時


プラグアンドプレイ Manager は、システムでプラグアンドプレイアクティビティが発生するたびに、IRP\_MJ\_PNP 要求を送信します。 その他のオペレーティングシステムコンポーネントおよびその他のカーネルモードドライバーは、マイナー関数コードに応じて、特定の IRP\_MJ\_PNP 要求を送信することもできます。

ドライバーのプラグアンドプレイの IRP 処理要件の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

IRP\_MJ\_PNP のマイナー関数コードに関する参照情報については、「[マイナー irp のプラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)」を参照してください。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムは、マイナー関数のコードを確認して、どの操作が要求されているかを判断する必要があります。 ファイルシステムでは、次のマイナー関数コードを処理する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
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

-   ユーザーによってボリュームが正常に削除されようとすると、PnP マネージャーは、\_デバイスの要求を削除\_、IRP\_\_クエリを送信します。 この IRP を受信すると、フィルターはボリューム上の開いているハンドルをすべて閉じ、スタック上の次の下位のドライバーに IRP を渡します。 これは非常に重要です。 ドライバーが開いているハンドルをすべて閉じるのに失敗した場合、ボリュームがマウント解除されないようにします。これにより、物理デバイスの取り出しを防止できます。

    &gt; \[!\_デバイス要求の削除\_IRP\_\_を正常に受信した &gt;\]、FAT ファイルシステムは、安全に削除できるすべてのボリュームを直ちにマウント解除します。 そのため、FAT ボリュームにアタッチされたフィルターは、フィルターの完了ルーチンが呼び出される前に、そのフィルターデバイスオブジェクトが解放されることを期待する必要があります。 NTFS ファイルシステムでは、この操作は行われません。 そのため、NTFS ボリュームにアタッチされたフィルターは、フィルターの完了ルーチンが呼び出されたときに、そのデバイスオブジェクトがボリュームにアタッチされることを期待できます。

     

-   Irp\_完了後に受信される Irp は、\_デバイスの要求を削除\_\_クエリを実行します。ただし、IRP\_が完了する前に、\_デバイスまたは IRP\_削除\_削除\_削除\_t_10_ DEVICE 要求を受信すると、スタックに安全に渡すことができます (ストレージデバイススタックによって失敗した場合)。または、削除またはデバイスの削除要求が受信されるまで、キューに保持できます。

-   フィルターが IRP\_完了した場合\_キャンセル\_\_デバイスの要求を削除します。 IRP\_に応答して、ボリュームの開いているハンドルをすべて閉じた後\_デバイスを削除\_ます。要求。ハンドルを再び開くことができます。 ただし、フィルターは、IRP がスタック内のドライバーによって正常に完了した後で、完了ルーチンでのみ実行できます。

-   フィルターが\_IRP を受信し、\_デバイスの要求\_削除すると、通常は irp に対して処理を実行する必要がありません。ただし、IRP\_完了した\_クエリを受信してから irp を保持している場合を除き\_\_デバイスの要求を削除します。 Irp がキューに保持されている場合、フィルターはそのボリュームのすべての Irp をデキューする必要があります。&gt;失敗した場合は、&lt;/i&gt; &lt;してから、IRP をスタック上の次の下位のドライバーに渡します。

-   \_予期しない IRP\_\_の削除要求を受信すると、フィルターは次の操作を実行します。

    -   未処理の参照がないまでファイルシステムがスタックをクリーンアップできないため、開いているすべてのハンドルをボリュームに対して閉じます。

    -   フィルターが Irp をキューに保持している場合は、エラーを発生させるか、スタックに渡すことができます (ストレージデバイススタックによって失敗する場合)。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、プラグアンドプレイ要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
PnP Irp の場合、このポインターは**NULL**である必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_PNP に指定します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかです。

-   IRP\_\_キャンセル\_\_デバイスの削除
-   IRP\_\_クエリ\_\_デバイスの削除
-   IRP\_\_\_デバイスの削除
-   \_デバイスを起動\_IRP\_
-   IRP\_\_驚く\_削除

## <a name="see-also"></a>関連項目


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_PNP (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_\_キャンセル\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)

[**IRP\_\_クエリ\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

[**IRP\_\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[ **\_デバイスを起動\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

[**IRP\_\_驚く\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

 

 






