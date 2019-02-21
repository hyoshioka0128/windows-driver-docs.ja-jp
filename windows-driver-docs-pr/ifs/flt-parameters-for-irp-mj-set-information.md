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
ms.openlocfilehash: 3645838be4647b01942340e9837c1099b5662e41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536004"
---
# <a name="fltparameters-for-irpmjsetinformation-union"></a>FLT\_IRP のパラメーター\_MJ\_設定\_情報共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_設定\_情報**](irp-mj-set-information.md)します。

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
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540232" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540232)"> <strong>FILE_ALLOCATION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545765" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545765)"> <strong>FILE_DISPOSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545780" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545780)"> <strong>FILE_END_OF_FILE_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540324" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540324)"> <strong>FILE_LINK_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540344" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540344)"> <strong>FILE_RENAME_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545873" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545873)"> <strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong> </a>ファイル。</p></td>
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
ファイルの終わりの操作のためのフラグ。 使用を指定します、 **EndOfFile**メンバー [**ファイル\_エンド\_の\_ファイル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545780)ときに構造体**FileInformationClass** == **FileEndOfFileInformation**します。 場合**TRUE**、設定は、ファイルの新しい有効なデータ長**EndOfFile**現在有効なデータの長さを増加している場合にのみです。 場合**FALSE**、新しいファイル サイズの設定から**EndOfFile**します。

**ClusterCount**  
システムの使用に予約されています。 使わないでください。

**DeleteHandle**  
システムの使用に予約されています。 使わないでください。

**InfoBuffer**  
設定するファイルの情報を含む入力バッファーへのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_設定\_操作には、パラメーターのセットの情報が含まれている情報コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_設定\_情報は IRP ベースの操作。

**AdvanceOnly**に設定されているメンバー **TRUE**を現在の有効なデータの長さをディスク上に新しい有効なデータ長に進み、ファイル システムに通知する、キャッシュ マネージャーによって**EndOfFile**. 場合**AdvanceOnly**は**FALSE**、新しいファイル サイズで、 **EndOfFile**現在のファイル サイズよりも大きくなることができます、メンバーが設定されています。

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


[**ファイル\_割り当て\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540232)

[**ファイル\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**ファイル\_廃棄\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545765)

[**ファイル\_エンド\_の\_ファイル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545780)

[**ファイル\_リンク\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540324)

[**ファイル\_位置\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**ファイル\_の名前を変更\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540344)

[**ファイル\_有効\_データ\_長さ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545873)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

 

 






