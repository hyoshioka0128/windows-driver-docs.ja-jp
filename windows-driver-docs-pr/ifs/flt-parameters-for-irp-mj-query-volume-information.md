---
title: FLT_PARAMETERS IRP_MJ_QUERY_VOLUME_INFORMATION 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_クエリ\_ボリューム\_情報。
ms.assetid: fc790885-a378-40dc-829d-94e75a7c6f13
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_VOLUME_INFORMATION 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 0b349d79a89b9e4ec9c11e61dd65a705277ca31d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571859"
---
# <a name="fltparameters-for-irpmjqueryvolumeinformation-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_ボリューム\_情報共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)します。

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

<a name="members"></a>メンバー
-------

**QueryVolumeInformation**  
次のメンバーを含む構造体。

**Length**  
バッファーの長さを (バイト単位) で**VolumeBuffer**します。

**FsInformationClass**  
ファイル システム ボリューム情報の種類。 次のいずれかです。

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
<td align="left"><a href="" id="filefsattributeinformation"></a>
<strong>FileFsAttributeInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540287" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540287)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a>ボリューム ラベル、シリアル番号、および作成時刻など、ボリュームに関する情報を格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefscontrolinformation"></a>
<strong>FileFsControlInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540258" data-raw-source="[&lt;strong&gt;FILE_FS_CONTROL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540258)"> <strong>FILE_FS_CONTROL_INFORMATION</strong> </a>ボリュームに関するファイル システムの制御情報を含む構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsdeviceinformation"></a>
<strong>FileFsDeviceInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545788" data-raw-source="[&lt;strong&gt;FILE_FS_DEVICE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545788)"> <strong>FILE_FS_DEVICE_INFORMATION</strong> </a>ボリュームのデバイス情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsdriverpathinformation"></a>
<strong>FileFsDriverPathInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540262" data-raw-source="[&lt;strong&gt;FILE_FS_DRIVER_PATH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540262)"> <strong>FILE_FS_DRIVER_PATH_INFORMATION</strong> </a>かどうか、指定したドライバーが、ボリュームの I/O パスに関する情報を含む構造体。 IRP_MJ_QUERY_VOLUME_INFORMATION 要求の発信元は、IRP をファイル システム ボリューム デバイス スタックに送信する前に、FILE_FS_DRIVER_PATH_INFORMATION 構造に、ドライバーの名前を格納する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefsfullsizeinformation"></a>
<strong>FileFsFullSizeInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540267" data-raw-source="[&lt;strong&gt;FILE_FS_FULL_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540267)"> <strong>FILE_FS_FULL_SIZE_INFORMATION</strong> </a>ボリュームで使用可能な領域の合計金額についての情報を含む構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsobjectidinformation"></a>
<strong>FileFsObjectIdInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540274" data-raw-source="[&lt;strong&gt;FILE_FS_OBJECTID_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540274)"> <strong>FILE_FS_OBJECTID_INFORMATION</strong> </a>ボリュームのファイル システム固有のオブジェクト ID 情報を含む構造体。 これはいないと同じで、(グローバル一意識別子 [GUID]-ベースの) オペレーティング システムが割り当てる一意なボリューム名。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssizeinformation"></a>
<strong>FileFsSizeInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540282" data-raw-source="[&lt;strong&gt;FILE_FS_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540282)"> <strong>FILE_FS_SIZE_INFORMATION</strong> </a> IRP_MJ_ を開始したスレッドに関連付けられているユーザーに提供される、ボリューム領域の量に関する情報を含む構造体QUERY_VOLUME_INFORMATION 要求。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="filefsvolumeinformation"></a>
<strong>FileFsVolumeInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540287" data-raw-source="[&lt;strong&gt;FILE_FS_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540287)"> <strong>FILE_FS_VOLUME_INFORMATION</strong> </a>ボリューム ラベル、シリアル番号、および作成時刻など、ボリュームに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="filefssectorsizeinformation"></a>
<strong>FileFsSectorSizeInformation</strong></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540262" data-raw-source="[&lt;strong&gt;FILE_FS_SECTOR_SIZE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540262)"> <strong>FILE_FS_SECTOR_SIZE_INFORMATION</strong> </a>ボリュームの物理および論理セクター サイズは、に関する情報を含む構造体。</p></td>
</tr>
</tbody>
</table>

 

**VolumeBuffer**  
ボリュームの情報が返される出力バッファーへのポインター。

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_クエリ\_ボリューム\_情報の操作には、パラメーターが含まれます。コールバック データによって表される IRP ベース ボリューム情報の照会操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_ボリューム\_情報は IRP ベースの操作。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

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

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)

 

 






