---
title: IRP_MJ_SET_INFORMATION
description: IRP\_MJ\_SET\_INFORMATION
ms.assetid: cc1b539c-8d39-4f4d-93b1-ce9fcdb8c555
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_SET_INFORMATION
topic_type:
- apiref
api_name:
- IRP_MJ_SET_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c834b9a5af5d0cbceab057523d94df06c5c2a30
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977657"
---
# <a name="irp_mj_set_information"></a>IRP\_MJ\_SET\_INFORMATION


## <a name="when-sent"></a>送信時


IRP\_MJ\_SET\_情報要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードのアプリケーションが**Setendoffile**などの Microsoft Win32 関数を呼び出したときや、カーネルモードのコンポーネントが[**Zwsetinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)を呼び出したときなどに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトを抽出してデコードし、ユーザーファイルまたはディレクトリが開いているかどうかを判断する必要があります。 存在する場合は、ファイルシステムドライバーが要求を適切に処理し、IRP を完了する必要があります。

ファイルとディレクトリには、次の種類の情報を設定できます。

FileBasicInformation

FileDispositionInformation

FileLinkInformation (ディレクトリ階層でサイクルを作成できるようにするファイルシステムの場合)

FilePositionInformation

FileRenameInformation

次の種類の情報は、ファイルに対してのみ設定できます。

Fileの情報

FileEndOfFileInformation

FileLinkInformation (NTFS などのファイルシステムの場合は、ディレクトリ階層内でサイクルを作成することはできません)

FileValidDataLengthInformation

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、set file information 要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
設定するファイルまたはディレクトリの情報が格納されている入力バッファーへのポインター。 この情報は、次のいずれかの構造に格納されます。

[**ファイル\_割り当て\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**ファイル\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**ファイル\_の後処理\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**ファイル\_\_ファイル\_情報の末尾\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**ファイル\_\_情報の名前変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**ファイル\_有効な\_データ\_の長さ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。 詳細については、 [**Zwsetinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)への*iostatusblock*パラメーターの説明を参照してください。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ の処理中に、ファイル\_オブジェクト構造の**参照フィールドが**無効になります。このフィールドは\_情報を設定し\_使用できません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*\_情報を設定\_IRP\_MJ を指定します。

<a href="" id="irpsp--parameters-setfile-advanceonly"></a>*Irpsp-&gt;Parameters. SetFile. AdvanceOnly*ファイルの終わり操作のフラグ。 これにより、 **Fileinformationclass** == **Fileendoffileinformation**の場合に、 [ **\_ファイル\_情報構造の\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information) 、 **endoffile**メンバーファイルの使用が決定されます。 **TRUE**の場合、ファイルの新しい有効なデータ長は、現在の有効なデータ長が増加した場合にのみ、 **endoffile**から設定されます。 **FALSE**の場合は、新しいファイルサイズが**endoffile**から設定されます。

<a href="" id="irpsp--parameters-setfile-clustercount"></a>*Irpsp-&gt;Parameters. SetFile. ClusterCount*システム用に予約されています。

<a href="" id="irpsp--parameters-setfile-deletehandle"></a>*Irpsp-&gt;Parameters. SetFile. DeleteHandle*システム用に予約されています。

<a href="" id="irpsp--parameters-setfile-fileinformationclass"></a>*Irpsp-&gt;パラメーター。 SetFile. FileInformationClass*ファイルに設定する情報の種類を指定します。 次のいずれかです。

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
<td align="left"><p><strong>Fileの情報</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)"><strong>FILE_ALLOCATION_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)"><strong>FILE_DISPOSITION_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)"><strong>FILE_END_OF_FILE_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)"><strong>FILE_LINK_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)"><strong>FILE_RENAME_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)"><strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong></a>を設定します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setfile-fileobject"></a>*Irpsp-&gt;Parameters. SetFile. FileObject*名前変更またはリンク操作に使用します。 *Irp-&gt;AssociatedIrp-&gt;FileName*に完全修飾ファイル名が含まれている場合、または*irp-&gt;&gt;AssociatedIrp Rootdirectory*が**NULL**以外の場合、このメンバーは、操作の対象となるファイルの親ディレクトリのファイルオブジェクトポインターになります。 それ以外の場合は**NULL**になります。

<a href="" id="irpsp--parameters-setfile-length"></a>*Irpsp-&gt;Parameters. SetFile. Length* *Irp&gt;AssociatedIrp*によってポイントされるバッファーの長さ (バイト単位)。

<a href="" id="irpsp--parameters-setfile-replaceifexists"></a>*Irpsp-&gt;Parameters. SetFile. 置換 Eifexists*同じ名前のファイルが既に存在する場合に、指定したファイルに置き換える必要があることを指定するには、 **TRUE**に設定します。 指定した名前のファイルが既に存在する場合に名前の変更操作が失敗する場合は、 **FALSE**に設定します。

<a name="remarks"></a>注釈
-------

**AdvanceOnly**メンバーは、ディスク上の現在の有効なデータ長を**endoffile**の新しい有効なデータ長に進めるようにファイルシステムに通知するために、キャッシュマネージャーによって**TRUE**に設定されます。 **AdvanceOnly**が**FALSE**の場合は、 **endoffile**メンバー内の新しいファイルサイズが、現在のファイルサイズより大きいまたは小さい値に設定されています。

## <a name="see-also"></a>「


[**ファイル\_割り当て\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**ファイル\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**ファイル\_の後処理\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**ファイル\_\_ファイル\_情報の末尾\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**ファイル\_\_情報の名前変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**ファイル\_有効な\_データ\_の長さ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)

 

 






