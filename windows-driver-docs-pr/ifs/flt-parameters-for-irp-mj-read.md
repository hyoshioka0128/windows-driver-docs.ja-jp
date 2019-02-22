---
title: FLT_PARAMETERS IRP_MJ_READ 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_読み取り。
ms.assetid: 48674db7-c0cc-45a0-bce9-eaf1a4cec362
keywords:
- FLT_PARAMETERS IRP_MJ_READ 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: b1ae103d05ffd2262ada7c8043809e7e39b97e07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560997"
---
# <a name="fltparameters-for-irpmjread-union"></a>FLT\_IRP のパラメーター\_MJ\_読み取り共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は構造体[ **IRP\_MJ\_読み取り**](irp-mj-read.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                   Length;
    ULONG POINTER_ALIGNMENT Key;
    LARGE_INTEGER           ByteOffset;
    PVOID                   ReadBuffer;
    PMDL                    MdlAddress;
  } Read;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**読み取り**  
次のメンバーを含む構造体。

**長さ**  
長さをバイト単位でデータを読み取る。

**キー**  
ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。

**ByteOffset**  
読み取るデータのファイル内のバイト オフセットを開始しています。

**ReadBuffer**  
ファイルから読み取られるデータを受信するバッファーへのポインター。

**MdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを**ReadBuffer**へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_読み取り操作には、コールバックのデータ (によって表される読み取り操作のパラメーターが含まれています。[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_IRP ベースの操作または I/O 操作が高速、読み取りができます。

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

[**FltReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff544286)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)

 

 






