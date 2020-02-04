---
title: IRP_MJ_QUERY_INFORMATION
description: IRP\_MJ\_QUERY\_INFORMATION
ms.assetid: d25bb277-e14c-4cd8-862a-46b4687bf539
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_QUERY_INFORMATION
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 010131afbfb16e8bc325417cfacbe7ee0d7158e7
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977673"
---
# <a name="irp_mj_query_information"></a>IRP\_MJ\_QUERY\_INFORMATION


## <a name="when-sent"></a>送信時


IRP\_MJ\_QUERY\_INFORMATION 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって、送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**GetFileInformationByHandle**などの Microsoft Win32 関数を呼び出したとき、またはカーネルモードコンポーネントが[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルまたはディレクトリが開いているユーザーを表すかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 その場合、ドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーはクエリを処理せずに、必要に応じて IRP を完了する必要があります。

クエリ可能なファイルとディレクトリの情報の種類は、ファイルシステムによって異なりますが、一般的には次のものが含まれます。

FileAllInformation FileAlternateNameInformation Fileallinformation FileBasicInformation FilecompresFileEaInformation information FileInternalInformation FileNameInformation FileNetworkOpenInformation FilePositionInformation FileStandardInformation FileStreamInformation File 情報。 FileAccessInformation、File、および FileModeInformation の情報は、パラメーターとして[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)に渡すこともできます。この情報は、ファイルシステムに依存しません。 このため、 **Zwqueryinformationfile**は、この情報を直接提供します。 IRP\_MJ\_クエリ\_情報要求をファイルシステムに送信する必要はありません。

これらの情報の種類の詳細については、以下の「関連項目」も参照してください。 使用可能なすべての情報の種類の一覧については、ntifs のファイル\_情報\_クラス列挙体を参照してください。

## <a name="operation-network-redirector-drivers"></a>操作: Network リダイレクタードライバー


IRP\_MJ\_QUERY\_INFORMATION request for FileAllInformation または FileNameInformation を受信する[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)に基づいていないネットワークリダイレクタードライバーは、サーバー名の前に1つの先頭に円記号が付いたファイル名の "\\サーバー\\共有\\ファイル" パスで応答する必要があります。 この名前情報の形式は、汎用名前付け規則 (UNC) 名としてアクセスされるファイル ( *\\\\サーバー\\共有\\フォルダー\\filename .txt*など)、またはマップされたドライブ (*x:\\フォルダー\\filename .txt*など) にあるファイルに対して返される必要があります。

ネットワークミニリダイレクタードライバー (rdbss と動的にリンクするドライバー、または rdbsslib と静的にリンクするドライバー) の場合、FileNameInformation に対する IRP\_MJ\_クエリ\_情報要求は RDBSS によって内部的に処理され、正しい名前情報が返されます。 ネットワークミニリダイレクタードライバーの場合は、IRP\_MJ\_QUERY\_INFORMATION request for FileAllInformation は、要求の名前情報部分に対して RDBSS によって内部的に処理されます。 FileAllInformation 要求のその他の部分は、ネットワークミニリダイレクタードライバーに対して、解決するために個別の要求として送信されます。

IRP\_MJ\_クエリ\_情報要求を受信するネットワークリダイレクターは、ファイルの短い名前が存在する場合は、パス情報を含まない短い名前 (8.3 文字) で応答する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーと、クエリファイル情報要求の処理での IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
ファイルまたはディレクトリの情報が返される出力バッファーへのポインター。 この情報は、次のいずれかの構造に格納されます。

すべての\_情報を\_ファイル

ファイル\_属性\_タグ\_情報

ファイル\_基本\_情報

ファイル\_の圧縮\_情報

ファイル\_EA\_情報

ファイル\_内部\_情報

ファイル\_名\_情報

ファイル\_ネットワーク\_\_情報を開く

ファイル\_位置\_情報

ファイル\_標準\_情報

ファイル\_ストリームの\_情報

ファイル\_リンク\_情報

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。 詳細については、 [**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)の*iostatusblock*パラメーターの説明を参照してください。 ルーチン.

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*I/o マネージャーによる i/o の完了時に、 *Irp&gt;AssociatedIrp*の内容をコピーする、呼び出し元から提供される出力バッファーへのポインター (省略可能)。 ドライバーは、このバッファーを使用して要求のデータを返しません。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_クエリ\_情報の処理中は、ファイル\_オブジェクト構造**の "参照**" フィールドは無効です。このフィールドは使用できません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*IRP\_MJ\_クエリ\_情報を指定します。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*Irpsp-&gt;Parameters. QueryFile. FileInformationClass*照会するファイル情報の種類。 このメンバーには、次のいずれかの値を指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ファイル</strong></p></td>
<td align="left"><p>ファイルの FILE_ALL_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)"><strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Filecompresの情報</strong></p></td>
<td align="left"><p>ファイルの FILE_COMPRESSION_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_EA_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)"><strong>FILE_INTERNAL_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)"><strong>FILE_NAME_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>ファイルの1つの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)"><strong>FILE_NETWORK_OPEN_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>ファイルの1つの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>ファイルの1つの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)"><strong>FILE_STANDARD_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>ファイルの1つの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)"><strong>FILE_STREAM_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Fileハードリンク情報</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information" data-raw-source="[&lt;strong&gt;FILE_LINKS_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)"><strong>FILE_LINKS_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*Irpsp-&gt;Parameters. QueryFile.* *Irp&gt;AssociatedIrp*によってポイントされるバッファーの長さ (バイト単位)。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_QUERY\_INFORMATION 操作は、常に i/o マネージャーによってバッファリングされます。 要求されたファイルまたはディレクトリの情報を返すために使用される*Irp&gt;AssociatedIrp*は、i/o マネージャーによって非ページプールメモリから割り当てられます。 その結果、オペレーティングシステムから返される*Irp&gt;AssociatedIrp*は、常に*irpsp-&gt;Parameters. queryfile.* の形式で指定された長さの有効なアドレスになります。

*Irp&gt;AssociatedIrp*は、i/o マネージャーによって内部的に使用されるため、ファイルシステムまたはファイルシステムフィルタードライバーでは使用できません。

## <a name="see-also"></a>「


[**ファイル\_アラインメント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_alignment_information)

[**ファイル\_属性\_タグ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)

[**ファイル\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**ファイル\_内部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)

[**ファイル\_名\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)

[**ファイル\_ネットワーク\_\_情報を開く**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**ファイル\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[**ファイル\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_設定\_情報**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






