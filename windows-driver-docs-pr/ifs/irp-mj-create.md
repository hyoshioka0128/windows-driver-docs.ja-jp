---
title: IRP_MJ_CREATE
description: IRP\_MJ\_CREATE
ms.assetid: fdcc81f0-e571-4194-88cd-d0956ca1577e
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_CREATE
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e88c2b95a573b693ad73fb7a562870a9c382c4
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852314"
---
# <a name="irp_mj_create"></a>IRP\_MJ\_CREATE


## <a name="when-sent"></a>送信時


I/o マネージャーは、 \_ \_ 新しいファイルまたはディレクトリが作成されているとき、または既存のファイル、デバイス、ディレクトリ、またはボリュームが開かれているときに、IRP MJ CREATE 要求を送信します。 通常、この IRP は、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)などの Microsoft Win32 関数を呼び出したユーザーモードアプリケーションの代わりに送信されるか、 [**iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**iocreatefilcreatedevice、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint) [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、または[**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)と呼ばれるカーネルモードコンポーネントの代わりに送信されます。 作成要求が正常に完了した場合、アプリケーションまたはカーネルモードコンポーネントは、ファイルオブジェクトへのハンドルを受け取ります。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合、ファイルシステムドライバーのディスパッチルーチンは、irp を完了し、適切な値に設定した後、適切な NTSTATUS*値を返す必要 &gt; *があります。 * &gt; *

それ以外の場合、ファイルシステムドライバーは作成要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーのディスパッチルーチンは、irp を完了し、適切な値に設定した後、適切な NTSTATUS*値を返す必要 &gt; *があります。 * &gt; *

それ以外の場合、フィルタードライバーは必要な処理を実行し、フィルターの性質に応じて、IRP を完了するか、スタック上の次の下位のドライバーに渡します。

一般に、フィルタードライバーは、 **IRP \_ MJ \_ CREATE**に応答して** \_ 保留状態**を返すことはできません。 ただし、下位レベルのドライバーから** \_ 保留状態**が返された場合、フィルタードライバーはこの状態値をドライバーチェーンに渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって[**IRP \_ MJ \_ CLEANUP**](irp-mj-cleanup.md)要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、 **IRP \_ MJ \_ create**以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、 **irp \_ MJ \_ CLEANUP**要求と[**irp \_ MJ \_ CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求を受け取ることを想定しています。 [**IocreatestreamfileMJ Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)の場合、 **IRP \_ \_ CLEANUP**要求は送信されません。

> [!NOTE]
> レガシフィルタードライバーが作成後のコールバックで作成を再発行する場合は、その再解析ポイント (補助バッファー) に関連付けられているバッファーを**NULL**に設定する必要があります。 レガシフィルタードライバーがこのバッファーを解放せず、 **NULL**に設定した場合、ドライバーはメモリをリークします。 フィルタマネージャはこれを実行するため、ミニフィルタドライバはこれを行う必要はありません。

 

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、create 要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt; AssociatedIrp*  
ファイルオブジェクトが拡張属性を持つファイルを表す場合は、ファイルの[** \_ 完全な \_ EA \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)を指すポインターです。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--flags"></a>*Irp- &gt; フラグ*  
この要求には、次のフラグが設定されています。

IRP の \_ 作成 \_ 操作

IRP \_ 遅延 \_ IO \_ 完了

IRP \_ 同期 \_ API

<a href="" id="irp--requestormode"></a>*Irp- &gt;Irp->requestormode*は、操作を要求したプロセスの実行モード ( **kernelmode で**または**モード**) を示します。 SL \_ FORCE \_ アクセス \_ チェックフラグが設定されている場合は、 * &gt; irp->requestormode*が kernelmode での場合でも、アクセスチェックを実行する必要があることに注意してください。

<a href="" id="irp--iostatus"></a>*Irp- &gt;* 最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造への iostatus ポインター。 この構造体の**情報**メンバーは、ファイルシステムによって次のいずれかの値に設定されます。

\_作成されたファイル

ファイル \_ が \_ \_ 存在しません

ファイル \_ が存在します

開かれたファイル \_

上書きされたファイル \_

ファイルの \_ 置き換え

<a href="" id="irp--overlay-allocationsize"></a>*Irp- &gt;* ファイルのサイズの初期割り当てサイズ (バイト単位)。 0以外の値は、ファイルが作成、上書き、または置き換えられない限り、無効です。

<a href="" id="irpsp--fileobject"></a>*Irpsp- &gt;* 作成または開くファイルを表すために I/o マネージャーによって作成されるファイルオブジェクトへの FileObject ポインター。 ファイルシステムは、IRP MJ CREATE 要求を処理するときに、 \_ \_ このファイルオブジェクトの**fscontext**および場合によっては**FsContext2**フィールドを、ファイルシステム固有の値に設定します。 このため、ファイルシステムによって create 要求が処理されるまで、 **Fscontext**フィールドと**FsContext2**フィールドの値を有効と見なすことはできません。 詳細については、「[ファイルストリーム、ストリームコンテキスト、およびストリームごとのコンテキスト](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)」を参照してください。

[**Fltcancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)および[**iocancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)は、 \_ \_ \_ ファイルオブジェクトの**Flags**フィールドに、FO ファイルオープンキャンセルフラグを設定します。 このフラグを設定すると、IRP \_ MJ \_ CREATE 要求が取り消され、このファイルオブジェクトに対して[**irp \_ MJ \_ CLOSE**](irp-mj-close.md)要求が発行されます。 作成要求がキャンセルされると、再発行することはできません。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイル**RelatedFileObject** \_ オブジェクト構造の関連する fileobject フィールドは、既に開いているファイルオブジェクトを基準として、特定のファイルが開かれていることを示すために使用されます。 これは通常、相対ファイルがディレクトリであることを示していますが、ストリームベースのファイルは、既にファイルのストリームを使用して開いている可能性があります。 ファイルオブジェクト構造の関連性のある**fileobject**フィールド \_ は、IRP MJ CREATE の処理中にのみ有効です \_ \_ 。

<a href="" id="irpsp--flags"></a>*Irpsp- &gt;* 次の1つ以上にフラグを追加します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_CASE_SENSITIVE</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイル名の比較では大文字と小文字が区別されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FORCE_ACCESS_CHECK</p></td>
<td align="left"><p>このフラグが設定されている場合、 <em> &gt; irp->requestormode</em>の値が<strong>kernelmode で</strong>の場合でもアクセスチェックを実行する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_OPEN_PAGING_FILE</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイルはページングファイルになります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_OPEN_TARGET_DIRECTORY</p></td>
<td align="left"><p>このフラグが設定されている場合は、ファイルの親ディレクトリを開く必要があります。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*Irpsp- &gt;MajorFunction*は、IRP MJ CREATE を指定し \_ \_ ます。

<a href="" id="irpsp--parameters-create-ealength"></a>*Irpsp- &gt;EaLength*で、バッファーのサイズ (バイト単位) を* &gt; AssociatedIrp*に変更します。 * &gt; AssociatedIrp*の値が**NULL**の場合、このメンバーは0である必要があります。

<a href="" id="irpsp--parameters-create-fileattributes"></a>*Irpsp- &gt;Parameters.* ファイルを作成または開くときに適用される属性フラグの fileattributes ビットマスク。 明示的に指定された属性は、ファイルが作成、置き換えられた場合、または上書きされた場合にのみ適用されます。 既定では、この値はファイル属性 NORMAL です。これは、 \_ \_ 他のフラグまたは互換性のあるフラグの論理和の組み合わせによってオーバーライドできます。 このメンバーは、 [**Iocreatefilを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)指定する*fileattributes*パラメーターに対応します。

<a href="" id="irpsp--parameters-create-options"></a>*Irpsp- &gt;Parameters。作成*またはファイルを開くときに適用されるオプションを指定するフラグのオプションビットマスク。ファイルが既に存在する場合に実行されるアクションも指定します。

このパラメーターの上位8ビットは、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)されたデバイス*の処理パラメーターに*対応します。

このメンバーの下位24ビットは、 *Createoptions*パラメーターに対応して[**iocreatefilを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)指定します。 ファイルのスキャンを実行するファイルシステムフィルターおよびミニフィルタードライバー (ウイルス対策プログラムなど) では、ファイルが OPLOCKED フラグの場合に特に注意する必要があり \_ \_ \_ ます。 このフラグが設定されている場合、フィルターでは、IRP \_ MJ の作成操作をブロックしたり、遅延させたりすることはできません \_ 。

\_ \_ \_ プリ作成 (ディスパッチ) パスに OPLOCKED フラグが設定されている場合、ファイルが完了すると、次のいずれかの種類の操作を開始できません。これは、oplock が解除される可能性があるためです。

IRP \_ MJ \_ CLEANUP irp \_ MJ \_ CREATE irp \_ MJ \_ FILE \_ SYSTEM \_ CONTROL IRP \_ MJ \_ FLUSH buffer \_ IRP \_ MJ \_ LOCK \_ CONTROL irp \_ MJ \_ READ irp \_ MJ \_ SET \_ INFORMATION irp \_ MJ \_ WRITE フィルターまたはミニフィルターでファイルの完了を受け入れることができない場合 \_ \_ \_ 、OPLOCKED フラグの場合、irp MJ CREATE 要求を完了する必要があり \_ \_ \_ ます状態共有 \_ 違反。

[ \_ \_ \_ 完了 (作成後)] パスに OPLOCKED フラグが設定されている場合、ファイルが完了すると、ファイルシステムが*Irp- &gt; iostatus. status*をステータス OPLOCK [ \_ \_ \_ \_ 進行中の状態] の値に設定しているかどうかを確認する必要があります。 この状態値が設定されていない場合は、フィルターがファイルに対して上記の操作のいずれかを開始することが安全です。 この状態値が設定されている場合、oplock はまだ解除されていないため、oplock 解除を引き起こす可能性がある操作をフィルターで開始することはできません。 したがって、次のいずれかの条件が満たされるまで、ファイルに対する上記のすべての操作をフィルターで延期する必要があります。

-   Oplock の所有者は、 \_ ファイルシステムに FSCTL oplock ブレーク確認要求を送信し \_ \_ ます。
-   フィルターまたはミニフィルター以外のシステムコンポーネントは、oplock の解除が完了するまで待機する必要がある i/o 要求 (IRP \_ MJ \_ READ や irp MJ WRITE など) をファイルシステムに送信し \_ \_ ます。 フィルターまたはミニフィルターは、この新しい操作のディスパッチ (または事前操作コールバック) ルーチンから上記の操作のいずれかを開始できます。これは、ディスパッチまたは preoperation コールバックルーチンが、oplock の解除が完了するまで待機状態になるためです。

<a href="" id="irpsp--parameters-create-securitycontext--accessstate"></a>*Irpsp- &gt;SecurityContext- &gt; *オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む[**アクセス \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造へのポインター。

<a href="" id="irpsp--parameters-create-securitycontext--desiredaccess"></a>*Irpsp- &gt;SecurityContext- &gt; DesiredAccess*アクセス \_ マスク構造を指定して、ファイルに要求されたアクセス権を指定します。 詳細については、 [**IocreatefilDesiredAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)パラメーターの説明を参照してください。 *DesiredAccess*

<a href="" id="irpsp--parameters-create-shareaccess"></a>*Irpsp- &gt;パラメーター。* ファイルに要求された共有アクセス権のアクセスビットマスクを作成します。 このメンバーがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)している場合は、*このパラメーターの*説明を参照してください。

## <a name="see-also"></a>関連項目


[**アクセス \_ マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**アクセスの \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**\_EA の完全な \_ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreissuesynchronousio)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**Iocreatefilの場合は、デバイスを Ioint にします。**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ の \_ クリーンアップ**](irp-mj-cleanup.md)

[**IRP \_ MJ \_ CLOSE**](irp-mj-close.md)

[**IRP \_ MJ \_ CREATE (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)

 

 






