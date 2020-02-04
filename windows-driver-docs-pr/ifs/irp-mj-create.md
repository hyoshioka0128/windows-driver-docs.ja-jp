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
ms.openlocfilehash: 0b6626a0bc3a480b6bef4cfb98ad0bf4a970d581
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977689"
---
# <a name="irp_mj_create"></a>IRP\_MJ\_CREATE


## <a name="when-sent"></a>送信時


I/o マネージャーは、新しいファイルまたはディレクトリが作成されているとき、または既存のファイル、デバイス、ディレクトリ、またはボリュームが開かれているときに、IRP\_MJ\_CREATE 要求を送信します。 通常、この IRP は、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)などの Microsoft Win32 関数を呼び出したユーザーモードアプリケーションの代わりに送信されるか、 [**iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**iocreatefilcreatedevice、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint) [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、または[**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)と呼ばれるカーネルモードコンポーネントの代わりに送信されます。 作成要求が正常に完了した場合、アプリケーションまたはカーネルモードコンポーネントは、ファイルオブジェクトへのハンドルを受け取ります。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合、 *irp-&gt;iostatus. Status*と*Irp-&gt;Iostatus. 情報*を適切な値に設定した後で、ファイルシステムドライバーのディスパッチルーチンが irp を完了し、適切な NTSTATUS 値を返す必要があります。

それ以外の場合、ファイルシステムドライバーは作成要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーのディスパッチルーチンは、irp を完了し、適切な値に設定した後に、適切な NTSTATUS 値を返す必要があります。これには、 *irp&gt;iostatus. Status*と*Irp-&gt;Iostatus. 情報*を指定します。

それ以外の場合、フィルタードライバーは必要な処理を実行し、フィルターの性質に応じて、IRP を完了するか、スタック上の次の下位のドライバーに渡します。

一般に、フィルタードライバーは、 **IRP\_MJ\_CREATE**に応答して、**状態\_PENDING**を返さないようにする必要があります。 ただし、下位レベルのドライバーから**status\_PENDING**が返された場合、フィルタードライバーはこの状態の値をドライバーチェーンに渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、 **IRP\_MJ\_create**以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 フィルター ドライバーを受信することはそのため**IRP\_MJ\_クリーンアップ**と[**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)未知のファイル オブジェクトを要求します。 場合に[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)、 **IRP\_MJ\_クリーンアップ**要求は送信されません。

&gt; \[!注\]&gt;とレガシ フィルター ドライバーを再実行の作成 をコールバックを作成後、リリースしに、再解析ポイント (補助バッファー) に関連付けられているバッファーを設定する必要がありますが**NULL**します。 レガシフィルタードライバーがこのバッファーを解放せず、 **NULL**に設定した場合、ドライバーはメモリをリークします。 フィルタマネージャはこれを実行するため、ミニフィルタドライバはこれを行う必要はありません。

 

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、create 要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
ファイルへのポインターは、ファイルオブジェクトが拡張属性を持つファイルを表している場合に、 [**EA\_の完全な\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)ます。 それ以外の場合、このメンバーは**NULL**に設定されます。

<a href="" id="irp--flags"></a>*Irp&gt;フラグ*  
この要求には、次のフラグが設定されています。

IRP\_\_操作の作成

IRP\_\_IO\_の完了を遅延します

IRP\_同期\_API

<a href="" id="irp--requestormode"></a>*Irp-&gt;irp->requestormode*操作を要求したプロセスの実行モード ( **kernelmode で**または**モード**) を示します。 SL\_強制\_アクセス\_チェックフラグが設定されている場合は、 *Irp-&gt;irp->requestormode*が kernelmode での場合でも、アクセスチェックを実行する必要があることに注意してください。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。 この構造体の**情報**メンバーは、ファイルシステムによって次のいずれかの値に設定されます。

ファイル\_作成済み

ファイル\_\_存在しません\_

ファイル\_存在します

ファイル\_開いています

上書きされたファイル\_

ファイル\_置き換え済み

<a href="" id="irp--overlay-allocationsize"></a>*Irp&gt;オーバーレイのサイズ*変更ファイルの初期割り当てサイズ (バイト単位)。 0以外の値は、ファイルが作成、上書き、または置き換えられない限り、無効です。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject*作成または開くファイルを表すために i/o マネージャーによって作成されるファイルオブジェクトへのポインター。 ファイルシステムが IRP\_MJ\_CREATE 要求を処理すると、このファイルオブジェクトの**Fscontext**および場合によっては**FsContext2**フィールドが、ファイルシステム固有の値に設定されます。 このため、ファイルシステムによって create 要求が処理されるまで、 **Fscontext**フィールドと**FsContext2**フィールドの値を有効と見なすことはできません。 詳細については、「[ファイルストリーム、ストリームコンテキスト、およびストリームごとのコンテキスト](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)」を参照してください。

[**Fltcancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)と[**iocancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)は、ファイルオブジェクトの**FLAGS**フィールドで、\_取り消されたフラグを開く\_\_ファイルを設定します。 このフラグを設定すると、IRP\_MJ\_CREATE 要求が取り消され、このファイルオブジェクトに対して[**irp\_MJ\_CLOSE**](irp-mj-close.md)要求が発行されることを示します。 作成要求がキャンセルされると、再発行することはできません。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 ファイル\_オブジェクト構造の関連するフィールドは、既に開いているファイルオブジェクトを基準にし**て、特定**のファイルが開かれていることを示すために使用されます。 これは通常、相対ファイルがディレクトリであることを示していますが、ストリームベースのファイルは、既にファイルのストリームを使用して開いている可能性があります。 ファイル\_オブジェクト構造の関連性のある**fileobject**フィールドは、IRP\_MJ\_CREATE の処理中にのみ有効です。

<a href="" id="irpsp--flags"></a>*Irpsp-&gt;フラグ*次の1つまたは複数を実行します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_CASE_SENSITIVE</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイル名の比較では大文字と小文字が区別されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FORCE_ACCESS_CHECK</p></td>
<td align="left"><p>このフラグが設定されている場合は、 <em>IRP-&gt;irp->requestormode</em>の値が<strong>kernelmode で</strong>の場合でもアクセスチェックを実行する必要があります。</p></td>
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

 

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*IRP\_MJ\_作成することを指定します。

<a href="" id="irpsp--parameters-create-ealength"></a>*Irpsp-&gt;パラメーター。 EaLength* *Irp&gt;AssociatedIrp*のバッファーのサイズ (バイト単位)。 *Irp-&gt;AssociatedIrp*の値が**NULL**の場合、このメンバーは0である必要があります。

<a href="" id="irpsp--parameters-create-fileattributes"></a>*Irpsp-&gt;パラメーター。 FileAttributes を作成します。* ファイルを作成または開くときに適用される属性フラグのビットマスク。 明示的に指定された属性は、ファイルが作成、置き換えられた場合、または上書きされた場合にのみ適用されます。 既定では、この値は FILE\_ATTRIBUTE\_NORMAL です。これは、他のフラグまたは互換性のあるフラグの論理和の組み合わせによってオーバーライドできます。 このメンバーは、 [**Iocreatefilを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)指定する*fileattributes*パラメーターに対応します。

<a href="" id="irpsp--parameters-create-options"></a>*Irpsp-&gt;パラメーター。作成. オプション*ファイルを作成または開くときに適用するオプション、およびファイルが既に存在する場合に実行するアクションを指定するフラグのビットマスク。

このパラメーターの上位8ビットは、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)されたデバイス*の処理パラメーターに*対応します。

このメンバーの下位24ビットは、 *Createoptions*パラメーターに対応して[**iocreatefilを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)指定します。 ファイルのスキャンを実行するファイルシステムフィルターおよびミニフィルタードライバー (ウイルス対策プログラムなど) では、OPLOCKED フラグが\_場合、ファイル\_完了\_に特に注意する必要があります。 このフラグが設定されている場合は、フィルターで IRP\_MJ\_作成操作をブロックしたり、遅延させたりすることはできません。

ファイル\_完了し\_場合、事前作成 (ディスパッチ) パスで\_OPLOCKED フラグが設定されていると、oplock が失われる可能性があるため、次のいずれの種類の操作も開始できません。

IRP\_MJ\_CLEANUP IRP\_MJ\_CREATE IRP\_MJ\_ファイル\_システム\_コントロール IRP\_MJ\_フラッシュ\_バッファー IRP\_MJ\_ロック\_コントロール IRP\_MJ\_読み取り IRP\_MJ\_設定\_情報 IRP\_MJ\_\_の場合、フィルターまたはミニフィルターがファイルを受け入れない場合は書き込み\_@no__OPLOCKED フラグ t_23_、IRP\_MJ\_CREATE 要求を完了する必要があります。状態は\_共有\_違反です。

\_完了 (作成後) パスで\_OPLOCKED フラグが設定されている場合\_ファイルが完了した場合、フィルターは、ファイルシステムが*Irp-&gt;iostatus. status*に設定されているかどうかを確認する必要があります\_oplock\_\_進行状況の状態の値。 この状態値が設定されていない場合は、フィルターがファイルに対して上記の操作のいずれかを開始することが安全です。 この状態値が設定されている場合、oplock はまだ解除されていないため、oplock 解除を引き起こす可能性がある操作をフィルターで開始することはできません。 したがって、次のいずれかの条件が満たされるまで、ファイルに対する上記のすべての操作をフィルターで延期する必要があります。

-   Oplock の所有者は、ファイルシステムに対して、FSCTL\_OPLOCK\_中断\_確認要求を送信します。
-   フィルターまたはミニフィルター以外のシステムコンポーネントは、oplock の解除が完了するまで待機する必要がある i/o 要求をファイルシステムに送信します (IRP\_MJ\_READ または IRP\_MJ\_WRITE など)。 フィルターまたはミニフィルターは、この新しい操作のディスパッチ (または事前操作コールバック) ルーチンから上記の操作のいずれかを開始できます。これは、ディスパッチまたは preoperation コールバックルーチンが、oplock の解除が完了するまで待機状態になるためです。

<a href="" id="irpsp--parameters-create-securitycontext--accessstate"></a>*Irpsp-&gt;パラメーター。 SecurityContext-&gt;AccessState*オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む、[**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインター。

<a href="" id="irpsp--parameters-create-securitycontext--desiredaccess"></a>*Irpsp-&gt;パラメーター。 SecurityContext-&gt;DesiredAccess*ファイルに要求されたアクセス権を指定して\_マスク構造にアクセスします。 詳細については、 [**IocreatefilDesiredAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)パラメーターの説明を参照してください。

<a href="" id="irpsp--parameters-create-shareaccess"></a>*Irpsp-&gt;パラメーター。作成します。* ファイルに要求された共有アクセス権のビットマスク。 このメンバーがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)している場合は、*このパラメーターの*説明を参照してください。

## <a name="see-also"></a>「


[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ **\_の状態へのアクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**ファイル\_EA\_の完全\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreissuesynchronousio)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_閉じる**](irp-mj-close.md)

[**IRP\_MJ\_CREATE (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)

 

 






