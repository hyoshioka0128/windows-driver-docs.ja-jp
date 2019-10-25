---
title: IRP_MJ_SET_INFORMATION 共用体の FLT_PARAMETERS
description: 操作の FLT\_IO\_パラメーター\_ブロック構造の MajorFunction フィールドが IRP\_MJ\_\_情報を設定している場合に使用される共用体コンポーネント。
ms.assetid: 860973bf-a98d-4495-9d6c-093ee985f360
keywords:
- IRP_MJ_SET_INFORMATION union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 78d44630a1fbb2741691dfb515d01122a4313044
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841351"
---
# <a name="flt_parameters-for-irp_mj_set_information-union"></a>IRP\_MJ の FLT\_パラメーター\_設定\_情報共用体


操作の[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが[**IRP\_MJ\_\_情報を設定**](irp-mj-set-information.md)している場合に使用される共用体コンポーネント。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                    Length;
    FILE_INFORMATION_CLASS POINTER_ALIGNMENT FileInformationClass;
    PFILE_OBJECT                             ParentOfTarget;
    union {
      struct {
        BOOLEAN ReplaceIfExists;
        BOOLEAN AdvanceOnly;
      };
      ULONG  ClusterCount;
      HANDLE DeleteHandle;
    };
    PVOID                                    InfoBuffer;
  } SetFileInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**SetFileInformation**  
次のメンバーを含む構造体。

**長さ**  
**インフォバッファー**に格納されているバッファーの長さ (バイト単位)。

**FileInformationClass**  
ファイルに設定する情報の種類。 次のいずれかです。

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

 

**ParentOfTarget**  
名前変更またはリンク操作に使用します。 **Infobuffer&gt;FileName**に完全修飾ファイル名が含まれている場合、または**Infobuffer&gt;Rootdirectory**が**NULL**以外の場合、このメンバーは、のターゲットであるファイルの親ディレクトリのファイルオブジェクトポインターになります。運用. それ以外の場合は**NULL**になります。

(*名前のない構造体*)  
次のメンバーを含む構造体。

**置換 Eifexists**  
名前変更またはリンク操作に使用します。 同じ名前のファイルが既に存在する場合に、指定したファイルに置き換えるように指定するには、 **TRUE**に設定します。 指定した名前のファイルが既に存在する場合に名前の変更またはリンク操作が失敗する場合は、 **FALSE**に設定します。

**AdvanceOnly**  
ファイルの終わり操作のフラグ。 これにより、 **Fileinformationclass** == **Fileendoffileinformation**の場合に、 [ **\_ファイル\_情報構造の\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information) 、 **endoffile**メンバーファイルの使用が決定されます。 **TRUE**の場合、ファイルの新しい有効なデータ長は、現在の有効なデータ長が増加した場合にのみ、 **endoffile**から設定されます。 **FALSE**の場合は、新しいファイルサイズが**endoffile**から設定されます。

**ClusterCount**  
システム用に予約されています。 使わないでください。

**DeleteHandle**  
システム用に予約されています。 使わないでください。

**インフォバッファー**  
設定するファイル情報を格納している入力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_SET\_INFORMATION 操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータによって表される設定情報操作のパラメーターが含まれています ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data))。データ. これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_SET\_情報は、IRP ベースの操作です。

**AdvanceOnly**メンバーは、ディスク上の現在の有効なデータ長を**endoffile**の新しい有効なデータ長に進めるようにファイルシステムに通知するために、キャッシュマネージャーによって**TRUE**に設定されます。 **AdvanceOnly**が**FALSE**の場合は、 **endoffile**メンバー内の新しいファイルサイズが、現在のファイルサイズより大きいまたは小さい値に設定されています。

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


[**ファイル\_割り当て\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_allocation_information)

[**ファイル\_基本\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**ファイル\_の後処理\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information)

[**ファイル\_\_ファイル\_情報の末尾\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_end_of_file_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_link_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**ファイル\_\_情報の名前変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_rename_information)

[**ファイル\_有効な\_データ\_の長さ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_valid_data_length_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_設定\_情報**](irp-mj-set-information.md)

 

 






