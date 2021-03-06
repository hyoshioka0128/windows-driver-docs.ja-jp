---
title: IRP_MJ_QUERY_INFORMATION
description: IRP\_MJ\_QUERY\_INFORMATION
ms.assetid: d25bb277-e14c-4cd8-862a-46b4687bf539
keywords:
- IRP_MJ_QUERY_INFORMATION インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719700c238e08ce3044b58e0a891e1d7dfd02acd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384818"
---
# <a name="irpmjqueryinformation"></a>IRP\_MJ\_QUERY\_INFORMATION


## <a name="when-sent"></a>送信時


IRP\_MJ\_クエリ\_I/O マネージャーとその他のオペレーティング システム コンポーネント、またはその他のカーネル モード ドライバーによる情報の要求が送信されます。 この要求を送信できますなど、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**GetFileInformationByHandle**カーネル モード コンポーネントが呼び出されたときまたは[ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ファイルまたはディレクトリのユーザーのオープンを表すかどうかを確認するファイル オブジェクトをデコードする必要があります。 場合は、ドライバーは、クエリの処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーでは、クエリを処理することがなく適切な IRP を完了する必要があります。

クエリを実行できるファイルとディレクトリの情報の種類はファイル システムに依存するが、通常、次が含まれます。

FileAllInformation FileAlternateNameInformation FileAttributeTagInformation FileBasicInformation FileCompressionInformation FileEaInformation FileInternalInformation FileNameInformation FileNetworkOpenInformationFilePositionInformation FileStandardInformation FileStreamInformation FileHardLinkInformation が FileAccessInformation、FileAlignmentInformation、および FileModeInformation 情報の種類はできるにパラメーターとして渡すことも[ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)、この情報は、ファイル システムに依存しません。 したがって**ZwQueryInformationFile** IRP を送信することがなく、直接この情報を提供\_MJ\_クエリ\_ファイル システムに情報の要求。

これらの情報の種類の詳細については、以下のリンクも「を参照してください。 すべての可能な情報の種類の一覧は、ファイルを参照してください。\_情報\_ntifs.h でクラスの列挙体。

## <a name="operation-network-redirector-drivers"></a>操作:ネットワーク リダイレクター ドライバー


基づかないネットワーク リダイレクター ドライバー [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library) IRP を受信する\_MJ\_クエリ\_FileAllInformation または FileNameInformation、情報の要求は、完全な"で応答する必要があります\\server\\共有\\ファイル"を先頭にバック スラッシュを単一サーバー名の前にファイル名のパス。 汎用名前付け規則 (UNC) 名としてアクセスされるファイルの名前については、この形式を返す必要がある ( *\\\\server\\共有\\フォルダー\\ファイル名.txt*など) またはマップされたドライブ上にあるファイル (*x:\\フォルダー\\ファイル名.txt*など)。

ネットワーク ミニ リダイレクター (rdbss.sys を動的にリンクするドライバーやドライバー rdbsslib.lib と静的にリンクする)、ドライバーの IRP\_MJ\_クエリ\_FileNameInformation の情報の要求が内部的に処理されますRDBSS と正しい名前では、情報が返されます。 ネットワークのミニ リダイレクター ドライバーは IRP\_MJ\_クエリ\_FileAllInformation の情報の要求は要求の名前情報の一部の RDBSS によって内部的に処理します。 FileAllInformation 要求の他の部分は、解決するのにはネットワーク ミニ リダイレクター ドライバーに個別の要求として送信されます。

IRP を受信するネットワーク リダイレクター\_MJ\_クエリ\_場合、短い名前、パス情報がないファイルの短い名前 (8.3) で FileAlternateNameInformation の情報の要求が応答する必要がありますファイルに存在します。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクエリ ファイルの情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ファイルまたはディレクトリの情報が返される出力バッファーへのポインター。 この情報は、次の構造体のいずれかに格納されます。

ファイル\_すべて\_情報

ファイル\_属性\_タグ\_情報

ファイル\_BASIC\_情報

ファイル\_圧縮\_情報

ファイル\_EA\_情報

ファイル\_内部\_情報

ファイル\_名前\_情報

ファイル\_ネットワーク\_オープン\_情報

ファイル\_位置\_情報

ファイル\_標準\_情報

ファイル\_ストリーム\_情報

ファイル\_リンク\_情報

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)に関する最終的な完了の状態および情報を受け取る、要求された操作。 詳細については、の説明を参照して、 *IoStatusBlock*パラメーター、 [ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)します。 ルーチンです。

<a href="" id="irp--userbuffer"></a>*Irp -&gt;UserBuffer*を呼び出し元が指定の出力バッファーへの省略可能なポインターの内容*Irp -&gt;AssociatedIrp.SystemBuffer* I/O マネージャーによって I/O の完了時にコピーされます。 ドライバーでは、要求のデータを返すこのバッファーは使用しません。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クエリ\_情報、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_クエリ\_情報。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*IrpSp -&gt;Parameters.QueryFile.FileInformationClass*クエリを実行するファイル情報の種類。 このメンバーは、次の値のいずれかを指定できます。

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
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_ALL_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information)"> <strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_COMPRESSION_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_EA_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information)"> <strong>FILE_INTERNAL_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information)"> <strong>FILE_NAME_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)"> <strong>FILE_NETWORK_OPEN_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)"> <strong>FILE_STANDARD_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)"> <strong>FILE_STREAM_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileHardLinkInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_links_information" data-raw-source="[&lt;strong&gt;FILE_LINKS_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_links_information)"> <strong>FILE_LINKS_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*IrpSp -&gt;Parameters.QueryFile.Length*によって指し示されるバッファーの長さをバイト単位で*Irp -&gt;AssociatedIrp.SystemBuffer*します。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_クエリ\_情報の操作は、I/O マネージャーによって必ずバッファーされます。 *Irp -&gt;AssociatedIrp.SystemBuffer*要求されたファイルを返すために使用するか、ディレクトリ情報が非ページ プール メモリから I/O マネージャーによって割り当てられています。 結果として、 *Irp -&gt;AssociatedIrp.SystemBuffer*オペレーティング システムによって返されるは常に有効なアドレスで指定された長さを*IrpSp-&gt;Parameters.QueryFile.Length*.

*Irp -&gt;AssociatedIrp.UserBuffer* I/O マネージャーによって内部的に使用し、ファイル システムまたはファイル システム フィルター ドライバーでは使用されません。

## <a name="see-also"></a>関連項目


[**ファイル\_配置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_alignment_information)

[**ファイル\_属性\_タグ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information)

[**ファイル\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

[**ファイル\_内部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information)

[**ファイル\_名前\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information)

[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)

[**ファイル\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)

[**ファイル\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_links_information)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






