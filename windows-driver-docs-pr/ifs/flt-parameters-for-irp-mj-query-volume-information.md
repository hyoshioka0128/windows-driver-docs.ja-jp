---
title: IRP_MJ_QUERY_VOLUME_INFORMATION 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、IRP\_MJ\_クエリ\_ボリューム\_情報です。
ms.assetid: fc790885-a378-40dc-829d-94e75a7c6f13
keywords:
- IRP_MJ_QUERY_VOLUME_INFORMATION union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd2de1034314d996d899a9ad78c83effe1a7757
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841357"
---
# <a name="flt_parameters-for-irp_mj_query_volume_information-union"></a>IRP\_MJ の FLT\_パラメーター\_クエリ\_ボリューム\_情報共用体


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、 [**IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                  Length;
    FS_INFORMATION_CLASS POINTER_ALIGNMENT FsInformationClass;
  } QueryVolumeInformation;
  PVOID  VolumeBuffer;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**QueryVolumeInformation**  
次のメンバーを含む構造体。

**長さ**  
**Volumebuffer**に格納されているバッファーの長さ (バイト単位)。

**FsInformationClass**  
ファイルシステムが返すボリューム情報の種類。 次のいずれかです。

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
<td align="left"><a href="" id="filefsattributeinformation"></a>
<strong>FileFsAttributeInformation</strong></td>
<td align="left"><p>ボリュームラベル、シリアル番号、作成時刻など、ボリュームに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)"><strong>FILE_FS_VOLUME_INFORMATION</strong></a>を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefscontrolinformation"></a>
<strong>FileFsControlInformation</strong></td>
<td align="left"><p>ボリュームに関するファイルシステムコントロール情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)"><strong>FILE_FS_CONTROL_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsdeviceinformation"></a>
<strong>FileFsDeviceInformation</strong></td>
<td align="left"><p>ボリュームのデバイス情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_fs_device_information)"><strong>FILE_FS_DEVICE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsdriverpathinformation"></a>
<strong>FileFsDriverPathInformation</strong></td>
<td align="left"><p>指定されたドライバーがボリュームの i/o パスにあるかどうかに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)"><strong>FILE_FS_DRIVER_PATH_INFORMATION</strong></a>構造体を返します。 IRP_MJ_QUERY_VOLUME_INFORMATION 要求の発信者は、IRP をファイルシステムボリュームのデバイススタックに送信する前に、ドライバーの名前を FILE_FS_DRIVER_PATH_INFORMATION 構造体に格納する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsfullsizeinformation"></a>
<strong>FileFsFullSizeInformation</strong></td>
<td align="left"><p>ボリュームで使用可能な領域の合計に関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_full_size_information)"><strong>FILE_FS_FULL_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsobjectidinformation"></a>
<strong>FileFsObjectIdInformation</strong></td>
<td align="left"><p>ボリュームのファイルシステム固有のオブジェクト ID 情報が格納されている<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)"><strong>FILE_FS_OBJECTID_INFORMATION</strong></a>構造体を返します。 これは、オペレーティングシステムによって割り当てられる (グローバル一意識別子 (GUID) ベースの) 一意のボリューム名と同じではないことに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssizeinformation"></a>
<strong>FileFsSizeInformation</strong></td>
<td align="left"><p>IRP_MJ_QUERY_VOLUME_INFORMATION 要求を発信したスレッドに関連付けられているユーザーが使用できるボリューム上の領域の量に関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_size_information)"><strong>FILE_FS_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsvolumeinformation"></a>
<strong>FileFsVolumeInformation</strong></td>
<td align="left"><p>ボリュームラベル、シリアル番号、作成時刻など、ボリュームに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_volume_information)"><strong>FILE_FS_VOLUME_INFORMATION</strong></a>を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssectorsizeinformation"></a>
<strong>FileFsSectorSizeInformation</strong></td>
<td align="left"><p>ボリュームの物理的および論理的なセクターのサイズに関する情報を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_driver_path_information)"><strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong></a>構造体を返します。</p></td>
</tr>
</tbody>
</table>

 

**VolumeBuffer**  
ボリューム情報が返される出力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_クエリ\_ボリューム\_情報操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータで表される irp ベースのクエリボリューム情報操作のパラメーターが含まれています ([**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_クエリ\_ボリューム\_情報は、IRP ベースの操作です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

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

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

 

 






