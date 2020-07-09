---
title: IRP_MJ_DIRECTORY_CONTROL (IFS)
description: IRP \_ MJ \_ DIRECTORY \_ コントロール
ms.assetid: cb1bed36-bcb5-419b-87ca-6d9107ece6d1
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_DIRECTORY_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_DIRECTORY_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27dad27ec40dd7da37269f66ee7a066f849e779c
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141328"
---
# <a name="irp_mj_directory_control-ifs"></a>IRP \_ MJ \_ DIRECTORY \_ コントロール (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ DIRECTORY \_ CONTROL 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが**ReaddirectoryFindNextVolumeMountPoint w**や**FindNextVolumeMountPoint**などの Microsoft Win32 関数を呼び出したときや、カーネルモードコンポーネントが[**zwquerydirectoryfile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)を呼び出したときなどに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、マイナー関数のコードを確認して、どのディレクトリ制御操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。

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
<td align="left"><p>IRP_MN_NOTIFY_CHANGE_DIRECTORY</p></td>
<td align="left"><p>ディレクトリへの変更の通知要求を示します。 通常、この要求をすぐに満たすのではなく、ファイルシステムドライバーが IRP をプライベートキューに保持します。 ディレクトリに変更が行われると、ファイルシステムドライバーは通知を実行し、デキューを実行して IRP を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DIRECTORY</p></td>
<td align="left"><p>ディレクトリクエリ要求を示します。 照会できる情報の種類は、ファイルシステムによって異なりますが、一般的には次のような情報が含まれます。</p>
FileFileIdBothDirectoryInformation Directoryinformation FileDirectoryInformation Filebothdirectoryinformation FileIdFullDirectoryInformation FileNamesInformation FileObjectIdInformation FileReparsePointInformation</td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> FileQuotaInformation information クラスは互換性のために残されています。 [**IRP \_代わりに、MJ \_ クエリ \_ クォータ**](irp-mj-query-quota.md)を使用する必要があります。

 

要求された操作を実行すると、ファイルシステムドライバーが IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、「ディレクトリ制御要求の処理」で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の関連性の**あるフィールド**は、 \_ IRP MJ DIRECTORY コントロールの処理中は無効である \_ ため、 \_ \_ 使用しないでください。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; フラグ*  
次のフラグは、IRP を使用 \_ したクエリディレクトリに設定でき \_ \_ ます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>インデックスが指定されているディレクトリのエントリから、 <em>Irpsp- &gt; Parameters. Querydirectory. fileindex</em>でスキャンを開始します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>ディレクトリの最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、以前の IRP_MN_QUERY_DIRECTORY 要求からスキャンを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>最初に見つかったエントリだけを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RETURN_ON_DISK_ENTRIES_ONLY</p></td>
<td align="left"><p>ディレクトリの仮想化またはジャストインタイム拡張を実行するすべてのフィルターに対して、要求をファイルシステムに渡し、現在ディスク上にあるエントリを返すように指示します。</p></td>
</tr>
</tbody>
</table>

 

次のフラグを設定することができます、IRP を \_ \_ 通知する \_ 変更 \_ ディレクトリです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_WATCH_TREE</p></td>
<td align="left"><p>このディレクトリのすべてのサブディレクトリも監視する必要がある場合は、 <strong>TRUE</strong>に設定します。 ディレクトリ自体だけを監視する場合は、 <strong>FALSE</strong>に設定します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ DIRECTORY コントロールを指定し \_ \_ ます。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; minorfunction*  
次のいずれか:

-   IRP \_ の \_ \_ 変更通知 \_ ディレクトリ
-   IRP の全 \_ \_ クエリの \_ ディレクトリ

<a href="" id="irpsp--parameters-notifydirectory-completionfilter"></a>*IrpSp- &gt; Parameters. NotifyDirectory. このフィルター*  
詳細については、 [**Fsrtlnotifyfullchangedirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)への参照*フィルター*パラメーターの説明を参照してください。

<a href="" id="irpsp--parameters-notifydirectory-length"></a>*IrpSp- &gt; Parameters. NotifyDirectory. Length*  
* &gt; UserBuffer*が指すバッファーの長さ (バイト単位)。

<a href="" id="irpsp--parameters-querydirectory-fileindex"></a>*IrpSp- &gt; Parameters. QueryDirectory. FileIndex*  
ディレクトリスキャンを開始するファイルのインデックス。 指定された SL \_ インデックスフラグが設定されていない場合は無視され \_ ます。 このパラメーターは、どの Win32 関数またはカーネルモードサポートルーチンでも指定できません。 現在、このファイルは、32ビットの NT ベースのプラットフォームのみに存在する NT 仮想 DOS コンピューター (NTVDM) によってのみ使用されます。 ファイルインデックスは NTFS などのファイルシステムに対して定義されていないことに注意してください。これは、親ディレクトリ内のファイルの位置が固定されておらず、並べ替え順序を維持するためにいつでも変更できることに注意してください。

<a href="" id="irpsp--parameters-querydirectory-fileinformationclass"></a>*IrpSp- &gt; Parameters. QueryDirectory. FileInformationClass*  
次に示す値のいずれかを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ファイルのディレクトリ情報 (& i)</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)"><strong>FILE_BOTH_DIR_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileDirectoryInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information" data-raw-source="[&lt;strong&gt;FILE_DIRECTORY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)"><strong>FILE_DIRECTORY_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFullDirectoryInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)"><strong>FILE_FULL_DIR_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileIdBothDirectoryInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_BOTH_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)"><strong>FILE_ID_BOTH_DIR_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileIdFullDirectoryInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information" data-raw-source="[&lt;strong&gt;FILE_ID_FULL_DIR_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)"><strong>FILE_ID_FULL_DIR_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNamesInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information" data-raw-source="[&lt;strong&gt;FILE_NAMES_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)"><strong>FILE_NAMES_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileObjectIdInformation</strong></p></td>
<td align="left"><p>各ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information" data-raw-source="[&lt;strong&gt;FILE_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)"><strong>FILE_OBJECTID_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileQuotaInformation</strong></p></td>
<td align="left"><p>この情報クラスは互換性のために残されています。 代わりに<a href="irp-mj-query-quota.md" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong></a>を使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileReparsePointInformation</strong></p></td>
<td align="left"><p>ディレクトリの1つの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information" data-raw-source="[&lt;strong&gt;FILE_REPARSE_POINT_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)"><strong>FILE_REPARSE_POINT_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-querydirectory-filename"></a>*IrpSp- &gt; Parameters. QueryDirectory. FileName*  
指定したディレクトリ内のファイルの名前 (省略可能)。

<a href="" id="irpsp--parameters-querydirectory-length"></a>*IrpSp- &gt; Parameters. QueryDirectory. Length*  
* &gt; UserBuffer*が指すバッファーの長さ (バイト単位)。

## <a name="see-also"></a>関連項目


[**\_両方の \_ DIR \_ 情報をファイルにする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**ファイル \_ ディレクトリ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**ファイルの \_ 完全な \_ ディレクトリ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**ファイル \_ ID \_ 両方の \_ DIR \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**ファイル \_ ID の \_ 完全な \_ ディレクトリ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**ファイル \_ 名の \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**ファイルの \_ OBJECTID \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**ファイルの \_ 再解析 \_ ポイント \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ クエリ \_ クォータ**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






