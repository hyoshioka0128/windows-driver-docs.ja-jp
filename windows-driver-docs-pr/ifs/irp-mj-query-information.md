---
title: IRP_MJ_QUERY_INFORMATION (IFS)
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
ms.openlocfilehash: 87ce2ddd39c4627a899838254c6fef04869974ba
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141242"
---
# <a name="irp_mj_query_information-ifs"></a>IRP \_ MJ \_ クエリ \_ 情報 (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ QUERY \_ INFORMATION 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって、送信されます。 この要求は、たとえば、ユーザーモードアプリケーションが**GetFileInformationByHandle**などの Microsoft Win32 関数を呼び出したとき、またはカーネルモードコンポーネントが[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルまたはディレクトリが開いているユーザーを表すかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 その場合、ドライバーはクエリを処理し、IRP を完了する必要があります。 それ以外の場合、ドライバーはクエリを処理せずに、必要に応じて IRP を完了する必要があります。

クエリ可能なファイルとディレクトリの情報の種類は、ファイルシステムによって異なりますが、一般的には次のものが含まれます。

FileAllInformation FileAlternateNameInformation Fileallinformation FileBasicInformation FilecompresFileEaInformation information FileInternalInformation FileNameInformation FileNetworkOpenInformation FilePositionInformation FileStandardInformation FileStreamInformation File の情報をパラメーターとして[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)に渡すこともできますが、この情報はファイルシステムに依存していません。 このため、 **Zwqueryinformationfile**は、IRP \_ MJ \_ QUERY \_ 情報要求をファイルシステムに送信することなく、この情報を直接提供します。

これらの情報の種類の詳細については、以下の「関連項目」も参照してください。 使用可能なすべての情報の種類の一覧については、 \_ ntifs のファイル情報クラス列挙体を参照してください \_ 。

## <a name="operation-network-redirector-drivers"></a>操作: Network リダイレクタードライバー


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)に基づいていないネットワークリダイレクタードライバーは、 \_ \_ \_ Fileallinformation または FileNameInformation に対する IRP MJ QUERY 情報要求を受信すると、 \\ \\ \\ サーバー名の前に1つの先頭に円記号が付いたファイル名の完全な "サーバー共有ファイル" パスで応答する必要があります。 この名前情報の形式は、汎用名前付け規則 (UNC) 名 (たとえば、* \\ \\ サーバー \\ 共有 \\ フォルダー \\filename.txt*) としてアクセスされるファイル、またはマップされたドライブ (*x: \\ folder \\filename.txt*など) にあるファイルに対して返される必要があります。

ネットワークミニリダイレクタードライバー (rdbss.sys と動的にリンクするドライバー、または rdbsslib を使用して静的にリンクするドライバー) の場合、 \_ \_ \_ FILENAMEINFORMATION に対する IRP MJ QUERY INFORMATION 要求は RDBSS によって内部的に処理され、正しい名前情報が返されます。 ネットワークミニリダイレクタードライバーの場合、 \_ \_ \_ FileAllInformation に対する IRP MJ QUERY INFORMATION 要求は、要求の名前情報部分に対して RDBSS によって内部的に処理されます。 FileAllInformation 要求のその他の部分は、ネットワークミニリダイレクタードライバーに対して、解決するために個別の要求として送信されます。

FileAlternateNameInformation に対する IRP MJ QUERY 情報要求を受信するネットワークリダイレクターは、ファイルの \_ \_ \_ 短い名前が存在する場合、パス情報を含まない短い名前 (8.3 文字) で応答する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーと、クエリファイル情報要求の処理での IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp &gt;AssociatedIrp.SystemBuffer*  
ファイルまたはディレクトリの情報が返される出力バッファーへのポインター。 この情報は、次のいずれかの構造に格納されます。

\_すべての情報をファイルに \_

ファイル \_ 属性 \_ タグ \_ 情報

ファイルの \_ 基本 \_ 情報

ファイルの \_ 圧縮 \_ 情報

ファイル \_ EA の \_ 情報

ファイルの \_ 内部 \_ 情報

ファイル \_ 名 \_ 情報

ファイル \_ ネットワークの \_ オープン \_ 情報

ファイルの \_ 位置 \_ 情報

ファイルの \_ 標準 \_ 情報

ファイル \_ ストリームの \_ 情報

ファイル \_ リンクの \_ 情報

<a href="" id="irp--iostatus"></a>*Irp- &gt;* 最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造への iostatus ポインター。 詳細については、 [**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)の*iostatusblock*パラメーターの説明を参照してください。 ルーチン.

<a href="" id="irp--userbuffer"></a>*Irp- &gt;UserBuffer* (省略可能) 呼び出し元から提供される出力バッファーへのポインター。 i/o マネージャーによる i/o の完了時に、 *Irp &gt;AssociatedIrp.Systembuffer*の内容がコピーされます。 ドライバーは、このバッファーを使用して要求のデータを返しません。

<a href="" id="irpsp--fileobject"></a>*Irpsp- &gt;* *DeviceObject*に関連付けられているファイルオブジェクトへの FileObject ポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の MJ **fileobject**フィールド \_ は、IRP のクエリ情報の処理中は無効であり、 \_ 使用でき \_ \_ ません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp- &gt;MajorFunction*は \_ 、IRP MJ クエリ情報を指定し \_ \_ ます。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*Irpsp- &gt;Parameters. QueryFile. FileInformationClass*種類のファイル情報を照会します。 このメンバーには、次のいずれかの値を指定できます。

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

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*Irpsp- &gt;パラメーター。* *Irp &gt;AssociatedIrp.Systembuffer*が指すバッファーの長さをバイト単位で格納します。

<a name="remarks"></a>解説
-------

IRP \_ MJ \_ QUERY \_ INFORMATION 操作は、常に i/o マネージャーによってバッファリングされます。 要求されたファイルまたはディレクトリの情報を返すために使用される*Irp &gt;AssociatedIrp.Systembuffer*は、i/o マネージャーによって非ページプールメモリから割り当てられます。 その結果、オペレーティングシステムから返された*Irp &gt;AssociatedIrp.Systembuffer*は、常に*Irpsp- &gt; Parameters. queryfile.* の長さの有効なアドレスになります。

* &gt; AssociatedIrp*は、i/o マネージャーによって内部的に使用され、ファイルシステムまたはファイルシステムフィルタードライバーでは使用できません。

## <a name="see-also"></a>関連項目


[**ファイルの \_ 配置 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_alignment_information)

[**ファイル \_ 属性 \_ タグ \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)

[**ファイルの \_ 基本 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**ファイルの \_ 内部 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)

[**ファイル \_ 名 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)

[**ファイル \_ ネットワークの \_ オープン \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**ファイルの \_ 位置 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**ファイルの \_ 標準 \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[**ファイル \_ ストリームの \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**ファイル \_ リンクの \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ の \_ 設定 \_ 情報**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 






