---
title: IRP_MJ_QUERY_VOLUME_INFORMATION
description: IRP\_MJ\_クエリ\_ボリューム\_情報
ms.assetid: 1e762c75-70bd-4397-b244-df97b317b3bf
keywords:
- IRP_MJ_QUERY_VOLUME_INFORMATION インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_VOLUME_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ead50b6913b1915b67aa4c8941885f5bd4003db6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384813"
---
# <a name="irpmjqueryvolumeinformation"></a>IRP\_MJ\_クエリ\_ボリューム\_情報


## <a name="when-sent"></a>送信時


**IRP\_MJ\_クエリ\_ボリューム\_情報**要求は I/O マネージャーによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**GetDiskFreeSpace**または**GetFileType**します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトかどうかをファイル オブジェクトをデコードする必要があります。 ボリュームを開きます (または、ボリューム上のオブジェクトの開いている) は、ハンドルで、要求が発行された場合は、ファイル システム ドライバーは要求を処理し、IRP を完了する必要があります。

それ以外の場合、ファイル システム ドライバーは、クエリが失敗して、IRP の完了する必要があります。

クエリを実行できるボリューム情報の種類はファイル システムに依存しますが、通常、次が含まれます。

FileFsAttributeInformation

FileFsDeviceInformation

FileFsSizeInformation

FileFsVolumeInformation

すべての可能な情報の種類の一覧は、次を参照してください。 *IrpSp -&gt;Parameters.QueryVolume.FsInformationClass*以下。

## <a name="operation-network-redirect-drivers"></a>操作:リダイレクトのネットワーク ドライバー


ファイルを含める必要があります、FileFsDeviceInformation の要求を受信するネットワーク リダイレクター\_リモート\_、オプションのいずれかとしてデバイス、 **DeviceCharacteristics**のメンバー、 [ **ファイル\_FS\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)返される構造体。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクエリのボリューム情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ボリュームの情報が返されるシステム指定の出力バッファーへのポインター。 この情報は、次の構造体のいずれかに格納されます。

ファイル\_FS\_属性\_情報

ファイル\_FS\_コントロール\_情報

ファイル\_FS\_デバイス\_情報

ファイル\_FS\_ドライバー\_パス\_情報

ファイル\_FS\_完全\_サイズ\_情報

ファイル\_FS\_OBJECTID\_情報

ファイル\_FS\_サイズ\_情報

ファイル\_FS\_ボリューム\_フラグ\_情報

ファイル\_FS\_ボリューム\_情報

ファイル\_FS\_セクター\_サイズ\_情報

FileFsVolumeFlagsInformation クラスと関連付けられている[**ファイル\_FS\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)構造体には、以降 Windows Vista で利用可能バージョン。

<a href="" id="------irp--iostatus"></a> *Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)に関する最終的な完了の状態および情報を受け取る、要求された操作。

<a href="" id="------irp--userbuffer"></a> *Irp -&gt;UserBuffer*を呼び出し元が指定の出力バッファーへの省略可能なポインターの内容*Irp -&gt;AssociatedIrp.SystemBuffer* I/O マネージャーによって I/O の完了時にコピーされます。 ドライバーでは、要求のデータを返すこのバッファーは使用しません。

<a href="" id="------irpsp--fileobject"></a> *IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_の処理中にオブジェクトの構造が有効なない**IRP\_MJ\_クエリ\_ボリューム\_情報**使用しないでください。

<a href="" id="------irpsp--majorfunction"></a> *IrpSp -&gt;MajorFunction*指定**IRP\_MJ\_クエリ\_ボリューム\_情報**します。

<a href="" id="------irpsp--parameters-queryvolume-fsinformationclass"></a> *IrpSp -&gt;Parameters.QueryVolume.FsInformationClass*ボリューム ファイル システムによって返される情報の種類を指定します。 このメンバーには、次のいずれかを指定できます。

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
<td align="left"><p><strong>FileFsAttributeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information" data-raw-source="[&lt;strong&gt;FILE_FS_ATTRIBUTE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information)"> <strong>FILE_FS_ATTRIBUTE_INFORMATION</strong> </a>属性については、ファイル システム ボリュームの責任を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>ボリュームに関するファイル システムの制御情報を含む構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsDeviceInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)"> <strong>FILE_FS_DEVICE_INFORMATION</strong> </a>ボリュームのデバイス情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsDriverPathInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information)"> <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> </a>かどうか、指定したドライバーが、ボリュームの I/O パスに関する情報を含む構造体。 発生元、 <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求に、ドライバーの名前を格納する必要があります、 <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> IRP をファイル システムに送信する前に構造体ボリューム デバイス スタックです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsFullSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information)"> <strong>FILE_FS_FULL_SIZE_INFORMATION</strong> </a>ボリュームで使用可能な領域の合計金額についての情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>ボリュームのファイル システム固有のオブジェクト ID 情報を含む構造体。 ないオペレーティング システムによって割り当てられた一意のボリュームを (GUID ベースの) 名前と同じに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information)"> <strong>FILE_FS_SIZE_INFORMATION</strong> </a> の発生元のスレッドに関連付けられているユーザーに提供される、ボリューム領域の量に関する情報を含む構造体<strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsVolumeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a>ボリューム ラベル、シリアル番号、および作成時刻などのボリュームに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSectorSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_sector_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_sector_size_information)"> <strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong> </a>ボリュームの物理および論理セクター サイズは、に関する情報を含む構造体。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="------irpsp--parameters-queryvolume-length"></a> *IrpSp -&gt;Parameters.QueryVolume.Length*によって指し示されるバッファーの長さをバイト単位で*Irp -&gt;UserBuffer*します。 返された場合は、この変数は、バッファーに書き込まれたバイト数を受け取ります。

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_属性\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_attribute_information)

[**ファイル\_FS\_コントロール\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_control_information)

[**ファイル\_FS\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_fs_device_information)

[**ファイル\_FS\_ドライバー\_パス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_fs_driver_path_information)

[**ファイル\_FS\_完全\_サイズ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_full_size_information)

[**ファイル\_FS\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_objectid_information)

**ファイル\_FS\_セクター\_サイズ\_情報**
[**ファイル\_FS\_サイズ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_size_information)

[**ファイル\_FS\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_fs_volume_information)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_設定\_ボリューム\_情報**](irp-mj-set-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






