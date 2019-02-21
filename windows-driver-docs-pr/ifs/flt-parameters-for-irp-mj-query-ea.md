---
title: FLT_PARAMETERS IRP_MJ_QUERY_EA 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_クエリ\_EA です。
ms.assetid: 858e8c72-33ae-441c-ada9-86c5df0e4f59
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_EA 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: c929e8e47829b85c33b8604bd422e28e9b17e70d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535407"
---
# <a name="fltparameters-for-irpmjqueryea-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_EA 共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                    Length;
    PVOID                    EaList;
    ULONG                    EaListLength;
    ULONG  POINTER_ALIGNMENT EaIndex;
    PVOID                    EaBuffer;
    PMDL                     MdlAddress;
  } QueryEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**QueryEa**  
次のメンバーを含む構造体。

**長さ**  
バッファーのバイト単位の長さを**EaBuffer**を指します。

**EaList**  
呼び出し元が指定へのポインター、ファイル\_取得\_EA\_情報構造化クエリを実行する拡張属性を指定する入力バッファー。

**EaListLength**  
バッファーのバイト単位の長さを**EaList**を指します。

**EaIndex**  
拡張属性の一覧をスキャンを開始する位置のエントリのインデックス。 場合、このパラメーターは無視されます、SL\_インデックス\_、FLT で指定したフラグが設定されていない\_IO\_パラメーター\_操作のブロック構造または**EaList**指す空でない一覧です。

**EaBuffer**  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545793)-拡張属性の値は返される構造化した出力バッファー。

**MdlAddress**  
バッファーを記述するメモリ記述子一覧 (MDL) のアドレスを**EaBuffer**を指します。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_クエリ\_EA** ](irp-mj-query-ea.md)操作にコールバック データによって表される IRP に基づくクエリの拡張-属性の情報操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_EA は IRP ベースの操作。

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

[**IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)

 

 






