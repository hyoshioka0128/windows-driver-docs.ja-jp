---
title: FLT_PARAMETERS IRP_MJ_SET_INFORMATION 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_設定\_情報。
ms.assetid: 860973bf-a98d-4495-9d6c-093ee985f360
keywords:
- FLT_PARAMETERS IRP_MJ_SET_INFORMATION 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 97377e2f3af757c4aa9d6fea04515da780e5a761
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380498"
---
# <a name="fltparameters-for-irpmjsetinformation-union"></a>FLT\_IRP のパラメーター\_MJ\_設定\_情報共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_設定\_情報**](irp-mj-set-information.md)します。

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
バッファーの長さを (バイト単位) で**InfoBuffer**します。

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
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information)"> <strong>FILE_ALLOCATION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information)"> <strong>FILE_DISPOSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)"> <strong>FILE_END_OF_FILE_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information)"> <strong>FILE_LINK_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information)"> <strong>FILE_RENAME_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>設定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information)"> <strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
</tbody>
</table>

 

**ParentOfTarget**  
名前の変更またはリンクの操作。 場合**InfoBuffer -&gt;ファイル名**、完全修飾ファイル名を含む場合、または**InfoBuffer -&gt;RootDirectory**以外**NULL**、このメンバーは、操作の対象となっているファイルの親ディレクトリのファイル オブジェクト ポインター。 それ以外の場合は**NULL**します。

(*構造体を無名*)  
次のメンバーを含む構造体。

**ReplaceIfExists**  
名前の変更またはリンクの操作。 設定**TRUE**に同じ名前の既存のファイルを指定されたファイルに置き換えられますことを指定します。 設定**FALSE**指定した名前のファイルが既に存在する場合、名前の変更またはリンクの操作が失敗する必要があります。

**AdvanceOnly**  
ファイルの終わりの操作のためのフラグ。 使用を指定します、 **EndOfFile**メンバー [**ファイル\_エンド\_の\_ファイル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)ときに構造体**FileInformationClass** == **FileEndOfFileInformation**します。 場合**TRUE**、設定は、ファイルの新しい有効なデータ長**EndOfFile**現在有効なデータの長さを増加している場合にのみです。 場合**FALSE**、新しいファイル サイズの設定から**EndOfFile**します。

**ClusterCount**  
システムの使用に予約されています。 使わないでください。

**DeleteHandle**  
システムの使用に予約されています。 使わないでください。

**InfoBuffer**  
設定するファイルの情報を含む入力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_設定\_操作には、パラメーターのセットの情報が含まれている情報コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_設定\_情報は IRP ベースの操作。

**AdvanceOnly**に設定されているメンバー **TRUE**を現在の有効なデータの長さをディスク上に新しい有効なデータ長に進み、ファイル システムに通知する、キャッシュ マネージャーによって**EndOfFile**. 場合**AdvanceOnly**は**FALSE**、新しいファイル サイズで、 **EndOfFile**現在のファイル サイズよりも大きくなることができます、メンバーが設定されています。

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


[**ファイル\_割り当て\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information)

[**ファイル\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

[**ファイル\_廃棄\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information)

[**ファイル\_エンド\_の\_ファイル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)

[**ファイル\_リンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information)

[**ファイル\_位置\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)

[**ファイル\_の名前を変更\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information)

[**ファイル\_有効\_データ\_長さ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

 

 






