---
title: IRP_MJ_SET_VOLUME_INFORMATION
description: IRP\_MJ\_\_ボリューム\_情報の設定
ms.assetid: 7c317e8b-ffa9-47f7-ac53-23b09873fab9
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_SET_VOLUME_INFORMATION
topic_type:
- apiref
api_name:
- IRP_MJ_SET_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e0d4858ae0134b4262112f4677534b0d3b24a0
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977671"
---
# <a name="irp_mj_set_volume_information"></a>IRP\_MJ\_\_ボリューム\_情報の設定


## <a name="when-sent"></a>送信時


IRP\_MJ\_SET\_VOLUME\_INFORMATION 要求は、i/o マネージャーによって送信されます。 たとえば、ユーザーモードアプリケーションが**SetVolumeLabel**などの Microsoft Win32 関数を呼び出したときに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、開いているユーザーボリュームを表すかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 存在する場合は、ファイルシステムドライバーが適切なボリューム情報を設定し、IRP を完了する必要があります。 それ以外の場合、ファイルシステムは、ボリューム情報を設定せずに、必要に応じて IRP を完了する必要があります。

設定できるボリューム情報の種類は、ファイルシステムによって異なりますが、一般的には次の1つ以上を含みます。

FileFsControlInformation

FileFsLabelInformation

FileFsObjectIdInformation

使用可能なすべての情報の種類の一覧については、ntifs の「FS\_INFORMATION\_クラス列挙体」を参照してください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、set volume information 要求の処理で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
設定するボリューム情報の値を格納している入力バッファーへのポインター。 この情報は、次のいずれかの構造に格納されます。

ファイル\_FS\_制御\_情報

ファイル\_FS\_ラベル\_情報

ファイル\_FS\_OBJECTID\_情報

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ の処理中に、ファイル\_オブジェクト構造**の "関連性のある"** フィールドは無効になります。\_ボリューム\_情報を\_設定して使用することはできません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*\_ボリューム\_情報を設定\_IRP\_MJ を指定します。

<a href="" id="irpsp--parameters-setvolume-fsinformationclass"></a>*Irpsp-&gt;Parameters. SetVolume. FsInformationClass*ボリュームに対して設定する情報の種類を指定します。 この値には、次のいずれかを指定できます。

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
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>ボリュームの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)"><strong>FILE_FS_CONTROL_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsLabelInformation</strong></p></td>
<td align="left"><p>ボリュームの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information" data-raw-source="[&lt;strong&gt;FILE_FS_LABEL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information)"><strong>FILE_FS_LABEL_INFORMATION</strong></a>を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>ボリュームの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)"><strong>FILE_FS_OBJECTID_INFORMATION</strong></a>を設定します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setvolume-length"></a>*Irpsp-&gt;Parameters. SetVolume. Length* *Irp&gt;AssociatedIrp*によってポイントされるバッファーの長さ (バイト単位)。

## <a name="see-also"></a>「


[**ファイル\_FS\_制御\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)

[**ファイル\_FS\_ラベル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information)

[**ファイル\_FS\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






