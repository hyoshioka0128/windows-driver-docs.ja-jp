---
title: IRP_MJ_CREATE
description: IRP\_MJ\_CREATE
ms.assetid: fdcc81f0-e571-4194-88cd-d0956ca1577e
keywords:
- Irp_mj_create 用インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4831e1e42e874eb3741b25bc42a956fa9ca1b46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376090"
---
# <a name="irpmjcreate"></a>IRP\_MJ\_CREATE


## <a name="when-sent"></a>送信時


I/O マネージャー送信 IRP\_MJ\_とき新しいファイルまたはディレクトリを作成中、またはデバイス、ディレクトリ、またはボリュームが開かれるときに、既存のファイル要求の作成。 通常この IRP をなど、Microsoft Win32 関数を呼び出すがユーザー モード アプリケーションに代わって送信[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)またはカーネル モード コンポーネントと呼ばれるに代わって[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)、 [ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)、 [ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)、または[ **ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)します。 作成要求が正常に完了すると、アプリケーションまたはカーネル モード コンポーネントでは、ファイル オブジェクトを識別するハンドルが受け取ります。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトの場合は、ファイル システム ドライバーのディスパッチ ルーチンする必要があります IRP を完了して、設定後、適切な NTSTATUS 値を返す*Irp -&gt;IoStatus.Status* *Irp -&gt;IoStatus.Information*適切な値にします。

それ以外の場合、ファイル システム ドライバーは、作成要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーのディスパッチ ルーチンする必要があります IRP を完了して、設定後、適切な NTSTATUS 値を返す対象のデバイス オブジェクトが、フィルター ドライバーの制御デバイス オブジェクトの場合は、 *Irp -&gt;IoStatus.Status*と*Irp -&gt;IoStatus.Information*適切な値にします。

それ以外の場合、フィルター ドライバーを必要な処理を実行し、フィルターの性質、によって IRP を完了するか、またはスタック上の次の下位ドライバーに渡します。

一般に、フィルター ドライバーは返されません**状態\_PENDING**への応答で**IRP\_MJ\_作成**です。 ただし、下位レベルのドライバーを返す場合**状態\_PENDING**、フィルター ドライバーがドライバーのチェーンには、この状態値を渡す必要があります。

ファイル システム フィルター ドライバー開発者が注意を[ **IoCreateStreamFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)により、 [ **IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)ボリュームのファイル システム ドライバー スタックに送信される要求。 ファイル システム多くの場合、オブジェクトを作成ストリーム ファイルの操作の副作用として以外のため、 **IRP\_MJ\_作成**ストリームのファイル オブジェクトの作成を確実に検出するために、フィルター ドライバーに対することは困難です。 フィルター ドライバーを受信することはそのため**IRP\_MJ\_クリーンアップ**と[**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)未知のファイル オブジェクトを要求します。 場合に[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)、 **IRP\_MJ\_クリーンアップ**要求は送信されません。

&gt; \[!注\]&gt;とレガシ フィルター ドライバーを再実行の作成 をコールバックを作成後、リリースしに、再解析ポイント (補助バッファー) に関連付けられているバッファーを設定する必要がありますが**NULL**します。 レガシ フィルター ドライバーのこのバッファーを解放しに設定はないかどうか**NULL**ドライバーのメモリがリークします。 ミニフィルター ドライバーは、フィルター マネージャーでは、これはそれらのため、このようにする必要はありません。

 

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所を作成する要求の処理では、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ポインターを[**ファイル\_完全\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)-構造化されたバッファーの場合は、ファイル オブジェクトが拡張属性を持つファイルを表します。 このメンバーに設定している場合は、 **NULL**します。

<a href="" id="irp--flags"></a>*Irp-&gt;フラグ*  
この要求に対して、次のフラグが設定されます。

IRP\_作成\_操作

IRP\_DEFER\_IO\_完了

IRP\_同期\_API

<a href="" id="irp--requestormode"></a>*Irp -&gt;requestormode で*か、操作を要求するプロセスの実行モードを示します**kernelmode である**または**UserMode**します。 場合に、SL に注意してください\_FORCE\_アクセス\_チェック フラグを設定、アクセス チェックを実行する必要があります、場合でも*Irp -&gt;requestormode で*は kernelmode であります。

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)に関する最終的な完了の状態および情報を受け取る、要求された操作。 ファイル システムのセット、**情報**値は次のいずれかに、この構造体のメンバー。

ファイル\_作成

ファイル\_は\_いない\_が存在

ファイル\_EXISTS

ファイル\_OPENED

ファイル\_OVERWRITTEN

ファイル\_優先

<a href="" id="irp--overlay-allocationsize"></a>*Irp -&gt;Overlay.AllocationSize*最初のファイルのバイト単位での割り当てサイズ。 0 以外の値及ぼしませんしない限り、ファイルが作成されている、上書き、または置き換えできます。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject* I/O マネージャーを作成または開かれたファイルを表す作成されたファイル オブジェクトへのポインター。 ファイル システムが IRP を処理するときに\_MJ\_作成要求、設定、 **FsContext**や**FsContext2**した値には、このファイル オブジェクトのフィールドファイル-システムに固有です。 値ではそのため、 **FsContext**と**FsContext2**フィールドできません有効と見なされるまで、ファイル システムの作成要求が処理した後。 詳細については、次を参照してください。[ファイル ストリーム、Stream のコンテキストや Stream あたり](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)します。

[**FltCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)と[ **IoCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocancelfileopen)設定、FO\_ファイル\_オープン\_ファイル オブジェクトの取り消し済みフラグ**フラグ**フィールド。 このフラグを設定することを示します IRP\_MJ\_作成要求が取り消され、および[ **IRP\_MJ\_閉じる**](irp-mj-close.md)の要求が発行されますこのファイル オブジェクト。 作成要求が取り消されとを再発行することはできません。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_オブジェクトの構造を使用して、ファイルが既に開かれているオブジェクトを基準として、指定されたファイルが開かれているを指定します。 これは通常、ファイルの既存のストリームの基準としたストリーム ベースのファイルを開くことができますが、相対的なファイルがディレクトリを示します。 **RelatedFileObject**ファイルのフィールド\_オブジェクトの構造は、IRP の処理中にのみ有効です\_MJ\_作成します。

<a href="" id="irpsp--flags"></a>*IrpSp -&gt;フラグ*次の 1 つ以上。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_CASE_SENSITIVE</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイル名の比較は大文字になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FORCE_ACCESS_CHECK</p></td>
<td align="left"><p>このフラグが設定されている場合、アクセス チェックが実行する必要がある場合でも、値の<em>IRP -&gt;requestormode で</em>は<strong>kernelmode である</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_OPEN_PAGING_FILE</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイルが、ページング ファイルを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_OPEN_TARGET_DIRECTORY</p></td>
<td align="left"><p>このフラグが設定されている場合、ファイルの親ディレクトリを開く必要があります。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_作成します。

<a href="" id="irpsp--parameters-create-ealength"></a>*IrpSp -&gt;Parameters.Create.EaLength* 、バッファーのバイト サイズ*Irp -&gt;AssociatedIrp.SystemBuffer*します。 場合の値*Irp -&gt;AssociatedIrp.SystemBuffer*は**NULL**、このメンバーは 0 である必要があります。

<a href="" id="irpsp--parameters-create-fileattributes"></a>*IrpSp -&gt;Parameters.Create.FileAttributes*作成またはファイルを開く際に適用する属性フラグのビット マスク。 明示的に指定された属性は、ファイルが作成、置き換え済み、または、場合によっては、上書きされる場合にのみ適用されます。 この値はファイルを既定では、\_属性\_NORMAL、または互換性フラグの論理和の組み合わせによって、他のフラグによってオーバーライドできます。 このメンバーに対応する、 *FileAttributes*パラメーターを[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。

<a href="" id="irpsp--parameters-create-options"></a>*IrpSp -&gt;Parameters.Create.Options*作成またはファイルが既に存在する場合に実行されるアクションと同様に、ファイルを開くときに適用されるオプションを指定するフラグのビットマスク。

このパラメーターの上位の 8 ビットに対応しています、*廃棄*パラメーターを[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。

このメンバーの下位 24 ビットに対応しています、 *CreateOptions*パラメーターを[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。 ファイル (ウイルス対策プログラム) などのスキャンを実行するファイル システム フィルターとミニフィルター ドライバーは、ファイルに特に注意を払う必要があります\_完了\_場合\_OPLOCKED フラグ。 フィルターのブロックまたはそれ以外の場合、IRP を遅延する必要がありますいないこのフラグが設定されている場合\_MJ\_作成操作です。

場合、ファイル\_完了\_場合\_(ディスパッチの作成) pre-create OPLOCKED フラグが設定パス、フィルター開始させては次の種類の操作のいずれかのため、oplock の中断が発生することができます。

IRP\_MJ\_クリーンアップ IRP\_MJ\_作成 IRP\_MJ\_ファイル\_システム\_コントロール IRP\_MJ\_フラッシュ\_バッファー IRP\_MJ\_ロック\_コントロール IRP\_MJ\_読み取り IRP\_MJ\_設定\_情報 IRP\_MJ\_かどうか、フィルターまたはミニフィルター優先できなくなり、ファイルを書き込む\_完了\_場合\_OPLOCKED フラグ、IRP を完了する必要があります\_MJ\_状態要求の作成\_共有\_違反が発生します。

場合、ファイル\_完了\_場合\_OPLOCKED フラグが設定が完了するまで (作成後の) パス、フィルター チェック ファイル システムが設定されているかどうか*Irp -&gt;IoStatus.Status*にステータス\_OPLOCK\_中断\_IN\_進行状況の状態の値。 この状態値が設定されていない場合は、ファイルでは、上記の操作のいずれかを開始するフィルターも安全です。 この状態値が設定されている場合は、oplock されていない、およびフィルターは、oplock を引き起こす可能性のあるすべての操作を開始する必要があります。 したがって、フィルターする必要があります延期ファイルでは、上記の操作はすべて、次の条件のいずれかが true になるまで。

-   Oplock の所有者に送信、FSCTL\_OPLOCK\_中断\_ファイル システムに要求を確認します。
-   フィルターまたはミニフィルター以外のシステム コンポーネントは、ファイル システムの oplock が完了するまで待機する必要がある I/O 要求を送信します (IRP など\_MJ\_読み取りまたは IRP\_MJ\_書き込み)。 フィルターまたはミニフィルターはこの新しい操作では、上記のディスパッチ (または preoperation コールバック) から操作ルーチンのいずれかをディスパッチまたは preoperation コールバック ルーチンは、oplock が完了するまで待機状態に配置されますので、開始することができます。

<a href="" id="irpsp--parameters-create-securitycontext--accessstate"></a>*IrpSp -&gt;Parameters.Create.SecurityContext -&gt;AccessState*へのポインター、 [**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)を含むオブジェクトの構造サブジェクト コンテキスト、付与されたアクセス型、および必要な残りの種類にアクセスします。

<a href="" id="irpsp--parameters-create-securitycontext--desiredaccess"></a>*IrpSp -&gt;Parameters.Create.SecurityContext -&gt;DesiredAccess*アクセス\_ファイルに対して要求されたアクセス権を指定するマスク構造体。 詳細については、の説明を参照して、 *DesiredAccess*パラメーターを[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。

<a href="" id="irpsp--parameters-create-shareaccess"></a>*IrpSp -&gt;Parameters.Create.ShareAccess*ファイルに、要求は共有アクセス権限のビットマスクを指定します。 このメンバーが 0 の場合は、排他的アクセスが要求されています。 詳細については、の説明を参照して、 *ShareAccess*パラメーターを[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。

## <a name="see-also"></a>関連項目


[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[**ファイル\_完全\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreissuesynchronousio)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocancelfileopen)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_(WDK カーネル リファレンス) を作成します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)

 

 






