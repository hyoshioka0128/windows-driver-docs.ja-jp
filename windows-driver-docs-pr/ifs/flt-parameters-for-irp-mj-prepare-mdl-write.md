---
title: FLT_PARAMETERS IRP_MJ_PREPARE_MDL_WRITE 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_準備\_MDL\_を記述します。
ms.assetid: eebbb8d4-f46d-4aee-aeb3-7edcbd23207a
keywords:
- FLT_PARAMETERS IRP_MJ_PREPARE_MDL_WRITE 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 00871879bfdcd2f0506aa4432e1cee1ad1c68ec5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530740"
---
# <a name="fltparameters-for-irpmjpreparemdlwrite-union"></a>FLT\_IRP のパラメーター\_MJ\_準備\_MDL\_書き込み共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は IRP を構造体\_MJ\_準備\_MDL\_を記述します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER           FileOffset;
    ULONG POINTER_ALIGNMENT Length;
    ULONG POINTER_ALIGNMENT Key;
    PMDL                    *MdlChain;
  } PrepareMdlWrite;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**PrepareMdlWrite**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内のバイトを開始しています。

**長さ**  
長さをバイト単位で、キャッシュされたファイルに書き込まれるデータ。

**キー**  
ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。 書き込まれる範囲と重複またはファイル内で排他的にロックされている範囲のサブ範囲には、このパラメーターはその排他ロックのキーである必要があります。 呼び出し元のスレッドの親プロセスが排他ロックを保持する必要があります。それ以外の場合、このパラメーターは無視されます。

**MdlChain**  
1 つまたは複数メモリ記述子のリスト (MDL) 書き込まれるデータを含むページを記述するのチェーンへのポインターを受け取る変数へのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_準備\_MDL\_書き込み操作には、高速のパラメーターが含まれていますI/O **PrepareMdlWrite**コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

場合、高速な I/O IRP\_MJ\_準備\_MDL\_書き込み要求が失敗した場合、I/O の発行者要求を再発行する方法を決定します。 ミニフィルターが常に利用できない IRP ベース IRP\_MJ\_MDL\_を記述します。 たとえば、IRP として IRP の要求を再発行する可能性があります\_MJ\_書き込み/IRP\_MN\_MDL します。

IRP\_MJ\_準備\_MDL\_書き込みの I/O 操作が高速です。

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

 

 






