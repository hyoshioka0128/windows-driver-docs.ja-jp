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
ms.openlocfilehash: 9070054ed8cb0026d527e8b119dcbf4419d08c07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324413"
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


ファイルを含める必要があります、FileFsDeviceInformation の要求を受信するネットワーク リダイレクター\_リモート\_、オプションのいずれかとしてデバイス、 **DeviceCharacteristics**のメンバー、 [ **ファイル\_FS\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545788)返される構造体。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクエリのボリューム情報の要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

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

FileFsVolumeFlagsInformation クラスと関連付けられている[**ファイル\_FS\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540287)構造体には、以降 Windows Vista で利用可能バージョン。

<a href="" id="------irp--iostatus"></a> *Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)に関する最終的な完了の状態および情報を受け取る、要求された操作。

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
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileFsAttributeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540251" data-raw-source="[&lt;strong&gt;FILE_FS_ATTRIBUTE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540251)"> <strong>FILE_FS_ATTRIBUTE_INFORMATION</strong> </a>属性については、ファイル システム ボリュームの責任を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsControlInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540258" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540258)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>ボリュームに関するファイル システムの制御情報を含む構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsDeviceInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545788" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545788)"> <strong>FILE_FS_DEVICE_INFORMATION</strong> </a>ボリュームのデバイス情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsDriverPathInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540262" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540262)"> <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> </a>かどうか、指定したドライバーが、ボリュームの I/O パスに関する情報を含む構造体。 発生元、 <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求に、ドライバーの名前を格納する必要があります、 <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> IRP をファイル システムに送信する前に構造体ボリューム デバイス スタックです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsFullSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540267" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540267)"> <strong>FILE_FS_FULL_SIZE_INFORMATION</strong> </a>ボリュームで使用可能な領域の合計金額についての情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsObjectIdInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540274" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540274)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>ボリュームのファイル システム固有のオブジェクト ID 情報を含む構造体。 ないオペレーティング システムによって割り当てられた一意のボリュームを (GUID ベースの) 名前と同じに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540282" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540282)"> <strong>FILE_FS_SIZE_INFORMATION</strong> </a> の発生元のスレッドに関連付けられているユーザーに提供される、ボリューム領域の量に関する情報を含む構造体<strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong>要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileFsVolumeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540287" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540287)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a>ボリューム ラベル、シリアル番号、および作成時刻などのボリュームに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileFsSectorSizeInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406395" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406395)"> <strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong> </a>ボリュームの物理および論理セクター サイズは、に関する情報を含む構造体。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="------irpsp--parameters-queryvolume-length"></a> *IrpSp -&gt;Parameters.QueryVolume.Length*によって指し示されるバッファーの長さをバイト単位で*Irp -&gt;UserBuffer*します。 返された場合は、この変数は、バッファーに書き込まれたバイト数を受け取ります。

## <a name="see-also"></a>関連項目


[**ファイル\_FS\_属性\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540251)

[**ファイル\_FS\_コントロール\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540258)

[**ファイル\_FS\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545788)

[**ファイル\_FS\_ドライバー\_パス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540262)

[**ファイル\_FS\_完全\_サイズ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540267)

[**ファイル\_FS\_OBJECTID\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540274)

**ファイル\_FS\_セクター\_サイズ\_情報**
[**ファイル\_FS\_サイズ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540282)

[**ファイル\_FS\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540287)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_設定\_ボリューム\_情報**](irp-mj-set-volume-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






