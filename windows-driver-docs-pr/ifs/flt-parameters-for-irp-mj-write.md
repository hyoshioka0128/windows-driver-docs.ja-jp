---
title: FLT_PARAMETERS IRP_MJ_WRITE 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_書き込み。
ms.assetid: c40d4c9e-2d09-4cd1-9278-5067dad2914f
keywords:
- FLT_PARAMETERS IRP_MJ_WRITE 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 1b0d96392670876e0076ee942404799064e61156
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393033"
---
# <a name="fltparameters-for-irpmjwrite-union"></a>FLT\_IRP のパラメーター\_MJ\_書き込み共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は構造体[ **IRP\_MJ\_書き込み**](irp-mj-write.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG         Length;
    ULONG         Key;
    LARGE_INTEGER ByteOffset;
    PVOID         WriteBuffer;
    PMDL          MdlAddress;
  } Write;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**書き込み**  
次のメンバーを含む構造体。

**長さ**  
長さをバイト単位で書き込まれるデータ。

**[キー]**  
ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。

**ByteOffset**  
書き込むデータのファイル内のバイト オフセットを開始しています。

**WriteBuffer**  
ファイルに書き込まれるデータを格納しているバッファーへのポインター。

**MdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを**WriteBuffer**へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_書き込み操作には、コールバックのデータ (によって表される、書き込み操作のパラメーターが含まれています。[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_書き込みが IRP ベース操作または I/O 操作が高速にすることができます。

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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff544610)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

[**ZwWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff567121)

 

 






