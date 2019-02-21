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
ms.openlocfilehash: fd9bf754c0259f4eda99951fb25d497fad05863d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536003"
---
# <a name="fltparameters-for-irpmjqueryinformation-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_情報共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)します。

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
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_ALL_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545750" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545750)"> <strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイルの構造体。</p></td>
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
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540318" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540318)"> <strong>FILE_INTERNAL_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileMoveClusterInformation</strong></p></td>
<td align="left"><p>ファイルの FILE_MOVE_CLUSTER_INFORMATION 構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545817" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545817)"> <strong>FILE_NAME_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://msdn.microsoft.com/library/windows/hardware/ff545822" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545822)"> <strong>FILE_NETWORK_OPEN_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://msdn.microsoft.com/library/windows/hardware/ff545855" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545855)"> <strong>FILE_STANDARD_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>1 つを返す<a href="https://msdn.microsoft.com/library/windows/hardware/ff540364" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540364)"> <strong>FILE_STREAM_INFORMATION</strong> </a>ファイルの構造体。</p></td>
</tr>
</tbody>
</table>

 

**InfoBuffer**  
ファイルの情報が返される出力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_クエリ\_情報の操作には、クエリはパラメーターが含まれています。コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_IRP ベース操作または高速な I/O 操作の情報を指定できます。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_属性\_タグ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545750)

[**ファイル\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**ファイル\_内部\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540318)

[**ファイル\_名前\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545817)

[**FILE\_NETWORK\_OPEN\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff545822)

[**ファイル\_位置\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

**ファイル\_位置\_情報**
[**ファイル\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545855)

[**ファイル\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540364)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

 

 






