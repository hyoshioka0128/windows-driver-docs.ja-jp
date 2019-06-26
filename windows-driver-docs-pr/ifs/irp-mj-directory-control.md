---
title: IRP_MJ_DIRECTORY_CONTROL
description: IRP\_MJ\_ディレクトリ\_コントロール
ms.assetid: cb1bed36-bcb5-419b-87ca-6d9107ece6d1
keywords:
- IRP_MJ_DIRECTORY_CONTROL インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_DIRECTORY_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfeba975abf3b203a0fdcd590c9cf82578a3459e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384833"
---
# <a name="irpmjdirectorycontrol"></a>IRP\_MJ\_ディレクトリ\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_ディレクトリ\_コントロール要求がや他のカーネル モード ドライバー I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**ReadDirectoryChangesW**または**FindNextVolumeMountPoint**またはカーネル モード コンポーネントが呼び出されたとき[ **ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーでは、必要なディレクトリ管理操作を決定するマイナー関数コードを確認する必要があります。 次に、有効なマイナー関数コードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_NOTIFY_CHANGE_DIRECTORY</p></td>
<td align="left"><p>ディレクトリへの変更を通知するための要求を示します。 通常、すぐにこの要求を満たす、代わりに、ファイル システム ドライバーを保持 IRP のプライベート キューでします。 ディレクトリに変更が発生したときに、ファイル システム ドライバーは、通知を実行し、デキューし、IRP を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DIRECTORY</p></td>
<td align="left"><p>ディレクトリのクエリ要求を示します。 クエリを実行できる情報の種類はファイル システムに依存しますが、通常、次が含まれます。</p>
FileBothDirectoryInformation FileDirectoryInformation FileFullDirectoryInformation FileIdBothDirectoryInformation FileIdFullDirectoryInformation FileNamesInformation FileObjectIdInformation FileReparsePointInformation</td>
</tr>
</tbody>
</table>

 

&gt; \[!注\] &gt; FileQuotaInformation 情報クラスは廃止されています。 [**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)代わりに使用する必要があります。

 

要求された操作を実行した後、ファイル システム ドライバーは IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所のディレクトリの管理要求の処理中に、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ディレクトリの内容に関する要求された情報を受け取る呼び出し元が指定の出力バッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_ディレクトリ\_コントロール、使用する必要があります。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
IRP の次のフラグを設定できます\_MN\_クエリ\_ディレクトリ。

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
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>指定するインデックスを持つディレクトリ内のエントリでスキャンを開始<em>IrpSp -&gt;Parameters.QueryDirectory.FileIndex</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>ディレクトリ内の最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、前の IRP_MN_QUERY_DIRECTORY 要求からのスキャンを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>見つかった最初のエントリのみを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RETURN_ON_DISK_ENTRIES_ONLY</p></td>
<td align="left"><p>ディレクトリの仮想化や現在ディスク上にあるエントリを単にファイル システムにを介して要求を受け渡すジャストイン タイムの拡張を実行するすべてのフィルターに指示します。</p></td>
</tr>
</tbody>
</table>

 

IRP の次のフラグを設定する\_MN\_通知\_変更\_ディレクトリ。

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
<td align="left"><p>SL_WATCH_TREE</p></td>
<td align="left"><p>設定<strong>TRUE</strong>場合もこのディレクトリのすべてのサブディレクトリを監視する必要があります。 設定<strong>FALSE</strong>ディレクトリ自体は、監視する場合のみです。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_ディレクトリ\_コントロール。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかです。

-   IRP\_MN\_通知\_変更\_ディレクトリ
-   IRP\_MN\_クエリ\_ディレクトリ

<a href="" id="irpsp--parameters-notifydirectory-completionfilter"></a>*IrpSp-&gt;Parameters.NotifyDirectory.CompletionFilter*  
詳細については、の説明を参照して、 *CompletionFilter*パラメーターを[ **FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)します。

<a href="" id="irpsp--parameters-notifydirectory-length"></a>*IrpSp-&gt;Parameters.NotifyDirectory.Length*  
によって示されるバッファーのバイト長*Irp -&gt;UserBuffer*します。

<a href="" id="irpsp--parameters-querydirectory-fileindex"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileIndex*  
ファイル ディレクトリのスキャンを開始する位置のインデックス。 場合は無視されます、SL\_インデックス\_指定されたフラグは設定されません。 このパラメーターは、任意の Win32 関数またはカーネル モードのサポート ルーチンでは指定できません。 現在、NT 仮想 DOS コンピューター (NTVDM) 32 ビット NT ベースのプラットフォームにのみ存在するによってのみ使用されます。 ファイルのインデックスは、NTFS を親ディレクトリ内のファイルの位置が固定されていないと、並べ替え順序を維持するために、いつでも変更できますなど、ファイル システムに対して定義されていないことに注意してください。

<a href="" id="irpsp--parameters-querydirectory-fileinformationclass"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileInformationClass*  
以下で説明する値のいずれかを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileBothDirectoryInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)"> <strong>FILE_BOTH_DIR_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileDirectoryInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information" data-raw-source="[&lt;strong&gt;FILE_DIRECTORY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)"> <strong>FILE_DIRECTORY_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFullDirectoryInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)"> <strong>FILE_FULL_DIR_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileIdBothDirectoryInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)"> <strong>FILE_ID_BOTH_DIR_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileIdFullDirectoryInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)"> <strong>FILE_ID_FULL_DIR_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNamesInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information" data-raw-source="[&lt;strong&gt;FILE_NAMES_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)"> <strong>FILE_NAMES_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileObjectIdInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information" data-raw-source="[&lt;strong&gt;FILE_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)"> <strong>FILE_OBJECTID_INFORMATION</strong> </a>ファイルごとに構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileQuotaInformation</strong></p></td>
<td align="left"><p>この情報クラスは廃止されています。 <a href="irp-mj-query-quota.md" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong> </a>代わりに使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileReparsePointInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information" data-raw-source="[&lt;strong&gt;FILE_REPARSE_POINT_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)"> <strong>FILE_REPARSE_POINT_INFORMATION</strong> </a>ディレクトリの構造体。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-querydirectory-filename"></a>*IrpSp-&gt;Parameters.QueryDirectory.FileName*  
指定したディレクトリ内のファイルの省略可能な名前です。

<a href="" id="irpsp--parameters-querydirectory-length"></a>*IrpSp-&gt;Parameters.QueryDirectory.Length*  
によって示されるバッファーのバイト長*Irp -&gt;UserBuffer*します。

## <a name="see-also"></a>関連項目


[**ファイル\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)

[**ファイル\_ディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)

[**ファイル\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)

[**ファイル\_ID\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)

[**ファイル\_ID\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)

[**ファイル\_名\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)

[**ファイル\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)

[**ファイル\_再解析\_ポイント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






