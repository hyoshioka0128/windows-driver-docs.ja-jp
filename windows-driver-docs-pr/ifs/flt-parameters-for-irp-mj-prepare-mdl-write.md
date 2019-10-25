---
title: IRP_MJ_PREPARE_MDL_WRITE 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造の MajorFunction フィールドが IRP\_MJ\_PREPARE\_MDL\_WRITE である場合に使用されます。
ms.assetid: eebbb8d4-f46d-4aee-aeb3-7edcbd23207a
keywords:
- IRP_MJ_PREPARE_MDL_WRITE union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 7ecac2eb0a8ec29bc823be0fbfa6f0c203185676
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841366"
---
# <a name="flt_parameters-for-irp_mj_prepare_mdl_write-union"></a>IRP\_MJ の FLT\_パラメーター\_準備\_MDL\_書き込み共用体


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MAJORFUNCTION**フィールドが IRP\_MJ\_PREPARE\_MDL\_WRITE である場合に使用されます。

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

**作成した Mdlwrite**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内の開始バイト。

**長さ**  
キャッシュされたファイルに書き込まれるデータの長さ (バイト単位)。

**Key**  
ターゲットファイルのバイト範囲ロックに関連付けられたキー値。 書き込まれる範囲がファイル内の排他的にロックされている範囲の場合、このパラメーターはその排他ロックのキーである必要があります。 排他ロックは、呼び出し元のスレッドの親プロセスによって保持されている必要があります。それ以外の場合、このパラメーターは無視されます。

**MdlChain**  
書き込むデータを含むページを記述する1つ以上のメモリ記述子リスト (MDL) のチェーンへのポインターを受け取る変数へのポインター。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_PREPARE\_MDL\_書き込み操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータによって表される高速な I/o/**書き込み**操作のパラメーターが含まれてい[ **\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

高速 i/o IRP\_MJ\_PREPARE\_MDL\_書き込み要求が失敗した場合は、i/o の発行者が要求を再発行する方法を決定します。 ミニフィルターでは、必ずしも IRP ベースの IRP\_MJ\_MDL\_書き込むことはできません。 たとえば、irp 要求は、IRP\_MJ\_WRITE/IRP\_\_MDL として再発行される可能性があります。

IRP\_MJ\_PREPARE\_MDL\_WRITE は高速な i/o 操作です。

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
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

 

 






