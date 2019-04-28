---
title: FLT_PARAMETERS IRP_MJ_SET_EA 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_設定\_EA です。
ms.assetid: 92136272-b40b-4f03-ab31-15184aaccd16
keywords:
- FLT_PARAMETERS IRP_MJ_SET_EA 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 883e422cca1d97b6b0958e18d859f1132ceafa09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361206"
---
# <a name="fltparameters-for-irpmjsetea-union"></a>FLT\_IRP のパラメーター\_MJ\_設定\_EA 共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_設定\_EA**](irp-mj-set-ea.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG Length;
    PVOID EaBuffer;
    PMDL  MdlAddress;
  } SetEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**SetEa**  
次のメンバーを含む構造体。

**長さ**  
バッファーのバイト単位の長さを**EaBuffer**を指します。

**EaBuffer**  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-拡張属性 (EA) を含む構造化の入力バッファーを設定する値します。

**MdlAddress**  
バッファーを記述するメモリ記述子一覧 (MDL) のアドレスを**EaBuffer**を指します。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_設定\_EA** ](irp-mj-set-ea.md)操作には、設定の拡張-属性-情報の操作にコールバック データによって表されるパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_設定\_EA は IRP ベースの操作。

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


[**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IoCheckEaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548252)

[**IRP\_MJ\_SET\_EA**](irp-mj-set-ea.md)

 

 






