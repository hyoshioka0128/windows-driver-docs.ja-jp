---
title: FLT_PARAMETERS IRP_MJ_MDL_READ 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_MDL\_読み取り。
ms.assetid: d07d3ba2-a405-481c-986b-7e26cda61909
keywords:
- FLT_PARAMETERS IRP_MJ_MDL_READ 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 27ea285278c3f719eaaafef443fb1e0150474861
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380331"
---
# <a name="fltparameters-for-irpmjmdlread-union"></a>FLT\_IRP のパラメーター\_MJ\_MDL\_読み取り共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作は IRP を構造体\_MJ\_MDL\_を読み取る。

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
  } MdlRead;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**MdlRead**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内のバイトを開始しています。

**長さ**  
長さをバイト単位で、キャッシュされたファイルから読み取られるデータ。

**[キー]**  
ターゲット ファイルのバイト範囲ロックに関連付けられているキーの値。 読み取る範囲と重複や、ファイル内で排他的にロックされている範囲のサブ範囲、このパラメーターはその排他ロックのキーである必要があります。 呼び出し元のスレッドの親プロセスが排他ロックを保持する必要があります。それ以外の場合、このパラメーターは無視されます。

**MdlChain**  
1 つ以上メモリ記述子のリスト (MDL) 読み取るデータを含むページを記述するのチェーンへのポインターを受け取る変数へのポインター。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_MDL\_読み取り操作が高速の I/O のパラメーターを含む**MdlRead**コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

場合、高速な I/O IRP\_MJ\_MDL\_読み取り要求が失敗した場合、I/O の発行者要求を再発行する方法を決定します。 ミニフィルターが常に利用できない IRP ベース IRP\_MJ\_MDL\_を読み取る。 たとえば、IRP として IRP の要求を再発行する可能性があります\_MJ\_読み取り/IRP\_MN\_MDL します。

IRP\_MJ\_MDL\_は高速な I/O 操作の読み取り。

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


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

 

 






