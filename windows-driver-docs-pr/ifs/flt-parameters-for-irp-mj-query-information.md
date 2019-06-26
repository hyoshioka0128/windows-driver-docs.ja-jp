---
title: FLT_PARAMETERS IRP_MJ_QUERY_INFORMATION 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_クエリ\_情報。
ms.assetid: 7fcd6881-1b6e-46eb-8476-d766f6fea7ef
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_INFORMATION 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: eaa82e67d2264a736be6b0d7fae7d89430e44ca9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375710"
---
# <a name="fltparameters-for-irpmjqueryinformation-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_情報共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                    Length;
    FILE_INFORMATION_CLASS POINTER_ALIGNMENT FileInformationClass;
    PVOID                                    InfoBuffer;
  } QueryFileInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**QueryFileInformation**  
次のメンバーを含む構造体。

**長さ**  
バッファーの長さを (バイト単位) で**InfoBuffer**します。

**FileInformationClass**  
返されるファイル情報の種類。 次のいずれかです。

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
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_ALL_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information)"> <strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_COMPRESSION_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_EA_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information)"> <strong>FILE_INTERNAL_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileMoveClusterInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_MOVE_CLUSTER_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information)"> <strong>FILE_NAME_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)"> <strong>FILE_NETWORK_OPEN_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)"> <strong>FILE_STANDARD_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)"> <strong>FILE_STREAM_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
</tbody>
</table>

 

**InfoBuffer**  
ファイルの情報が返される出力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_クエリ\_情報の操作には、クエリはパラメーターが含まれています。コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_IRP ベース操作または高速な I/O 操作の情報を指定できます。

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


[**ファイル\_属性\_タグ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_attribute_tag_information)

[**ファイル\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

[**ファイル\_内部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_internal_information)

[**ファイル\_名前\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_name_information)

[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_network_open_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)

**ファイル\_位置\_情報**
[**ファイル\_標準\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_standard_information)

[**ファイル\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

 

 






