---
title: IRP_MJ_SET_VOLUME_INFORMATION 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネント\_は、\_ボリューム\_情報を設定します。
ms.assetid: 316ce14c-02ea-45ab-8a2f-1b096f631d23
keywords:
- IRP_MJ_SET_VOLUME_INFORMATION union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 7175be67e12802bd9a08ea2aaba870b97771b4f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841343"
---
# <a name="flt_parameters-for-irp_mj_set_volume_information-union"></a>IRP\_MJ の FLT\_パラメーター\_設定\_ボリューム\_情報共用体


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネント\_は、 [ **\_ボリューム\_情報を設定**](irp-mj-set-volume-information.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                  Length;
    FS_INFORMATION_CLASS POINTER_ALIGNMENT FsInformationClass;
    PVOID                                  VolumeBuffer;
  } SetVolumeInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**SetVolumeInformation**  
次のメンバーを含む構造体。

**長さ**  
**Volumebuffer**に格納されているバッファーの長さ (バイト単位)。

**FsInformationClass**  
ボリュームに対して設定する情報の種類。 次のいずれかです。

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

 

**VolumeBuffer**  
設定するボリューム情報の値を格納している入力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

[**IRP\_MJ\_設定\_ボリューム\_情報**](irp-mj-set-volume-information.md)操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータによって表されるセットボリューム情報操作のパラメーターが含まれています ([**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_設定\_ボリューム\_情報は、IRP ベースの操作です。

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


[**ファイル\_FS\_制御\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_fs_control_information)

[**ファイル\_FS\_ラベル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_label_information)

[**ファイル\_FS\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_fs_objectid_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_\_ボリューム\_情報の設定**](irp-mj-set-volume-information.md)

[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)

 

 






