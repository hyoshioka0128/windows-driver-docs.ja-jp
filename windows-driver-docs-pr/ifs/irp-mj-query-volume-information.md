---
title: IRP_MJ_QUERY_VOLUME_INFORMATION
description: IRP\_MJ\_クエリ\_ボリューム\_情報
ms.assetid: 1e762c75-70bd-4397-b244-df97b317b3bf
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_QUERY_VOLUME_INFORMATION
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3381954c99c37221f4c6a8e096a395676ec4a28b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841172"
---
# <a name="irp_mj_query_volume_information"></a>IRP\_MJ\_クエリ\_ボリューム\_情報


## <a name="when-sent"></a>送信時


**IRP\_MJ\_QUERY\_VOLUME\_INFORMATION**要求は、i/o マネージャーによって送信されます。 たとえば、ユーザーモードアプリケーションが**Getdiskfreespace**領域や**Getfiletype**などの Microsoft Win32 関数を呼び出した場合に、これを送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトであるかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 その場合、またはボリュームが開いているハンドル (またはボリューム上のオブジェクトが開いているハンドル) で要求が発行されている場合は、ファイルシステムドライバーが要求を処理し、IRP を完了する必要があります。

それ以外の場合、ファイルシステムドライバーはクエリを失敗させ、IRP を完了する必要があります。

クエリ可能なボリューム情報の種類は、ファイルシステムによって異なりますが、一般的には次のようなものがあります。

FileFsAttributeInformation

FileFsDeviceInformation

FileFsSizeInformation

FileFsVolumeInformation

使用可能なすべての情報の種類の一覧については、以下の「 *Irpsp-&gt;Parameters* 」を参照してください。

## <a name="operation-network-redirect-drivers"></a>操作: ネットワークリダイレクトドライバー


FileFsDeviceInformation の要求を受信するネットワークリダイレクターは、ファイル[ **\_FS\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)構造の**DeviceCharacteristics**メンバーのオプションの1つとして、ファイル\_リモート\_デバイスを含める必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、IRP の次のメンバーと IRP スタックの場所に設定されている情報を、クエリボリューム情報要求の処理に使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
ボリューム情報が返されるシステム提供の出力バッファーへのポインター。 この情報は、次のいずれかの構造に格納されます。

ファイル\_FS\_属性\_情報

ファイル\_FS\_制御\_情報

ファイル\_FS\_デバイス\_情報

ファイル\_FS\_ドライバー\_パス\_情報

ファイル\_FS\_完全な\_サイズ\_情報

ファイル\_FS\_OBJECTID\_情報

ファイル\_FS\_サイズ\_情報

ファイル\_FS\_ボリューム\_フラグ\_情報

ファイル\_FS\_ボリューム\_情報

ファイル\_FS\_セクタ\_サイズ\_情報

FileFsVolumeFlagsInformation クラスと関連付けられている[**ファイル\_FS\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)構造は、Windows Vista 以降のバージョンで使用できます。

<a href="" id="------irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="------irp--userbuffer"></a>*Irp-&gt;UserBuffer*I/o マネージャーによる i/o の完了時に、 *Irp&gt;AssociatedIrp*の内容をコピーする、呼び出し元から提供される出力バッファーへのポインター (省略可能)。 ドライバーは、このバッファーを使用して要求のデータを返しません。

<a href="" id="------irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 **IRP\_MJ\_QUERY\_ボリューム\_情報**の処理中**は、ファイル**\_オブジェクト構造の関連性のあるフィールドは無効であり、使用できません。

<a href="" id="------irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction***IRP\_MJ\_クエリ\_ボリューム\_情報**を指定します。

<a href="" id="------irpsp--parameters-queryvolume-fsinformationclass"></a>*Irpsp-&gt;Parameters. QueryVolume. FsInformationClass*ファイルシステムによって返されるボリューム情報の種類を指定します。 このメンバーは、次のいずれかになります。

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
<td align="left"><p><strong>FileFsAttributeInformation</strong></p></td>
<td align="left"><p>ボリュームを担当するファイルシステムに関する属性情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information" data-raw-source="[&lt;strong&gt;FILE_FS_ATTRIBUTE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information)"><strong>FILE_FS_ATTRIBUTE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>ボリュームに関するファイルシステムコントロール情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)"><strong>FILE_FS_CONTROL_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsDeviceInformation</strong></p></td>
<td align="left"><p>ボリュームのデバイス情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)"><strong>FILE_FS_DEVICE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsDriverPathInformation</strong></p></td>
<td align="left"><p>指定されたドライバーがボリュームの i/o パスにあるかどうかに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)"><strong>FILE_FS_DRIVER_PATH_INFORMATION</strong></a>構造体を返します。 <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求の発信者は、IRP をファイルシステムボリュームのデバイススタックに送信する前に、そのドライバーの名前を<strong>FILE_FS_DRIVER_PATH_INFORMATION</strong>構造体に格納する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsFullSizeInformation</strong></p></td>
<td align="left"><p>ボリューム上で使用可能な領域の合計量に関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information)"><strong>FILE_FS_FULL_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>ボリュームのファイルシステム固有のオブジェクト ID 情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)"><strong>FILE_FS_OBJECTID_INFORMATION</strong></a>構造体を返します。 これは、オペレーティングシステムによって割り当てられる (GUID ベースの) 一意のボリューム名と同じではないことに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSizeInformation</strong></p></td>
<td align="left"><p><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求を発信したスレッドに関連付けられているユーザーが使用できるボリューム上の領域の量に関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information)"><strong>FILE_FS_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsVolumeInformation</strong></p></td>
<td align="left"><p>ボリュームラベル、シリアル番号、作成時刻などのボリュームに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)"><strong>FILE_FS_VOLUME_INFORMATION</strong></a>を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSectorSizeInformation</strong></p></td>
<td align="left"><p>ボリュームの物理的および論理的なセクターサイズに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_sector_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_sector_size_information)"><strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="------irpsp--parameters-queryvolume-length"></a>*Irpsp-&gt;パラメーター。 QueryVolume.* *Irp&gt;UserBuffer*が指すバッファーの長さ (バイト単位)。 返されると、この変数はバッファーに書き込まれたバイト数を受け取ります。

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_属性\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_attribute_information)

[**ファイル\_FS\_制御\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)

[**ファイル\_FS\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)

[**ファイル\_FS\_ドライバー\_パス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)

[**ファイル\_FS\_完全な\_サイズ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information)

[**ファイル\_FS\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)

**ファイル\_fs\_セクタ\_サイズ\_情報**
[**ファイル\_FS\_サイズ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information)

[**ファイル\_FS\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_\_ボリューム\_情報の設定**](irp-mj-set-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






