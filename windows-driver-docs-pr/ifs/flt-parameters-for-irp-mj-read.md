---
title: IRP_MJ_READ 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造体で、操作のブロック構造が IRP\_MJ\_READ になっている場合に使用されます。
ms.assetid: 48674db7-c0cc-45a0-bce9-eaf1a4cec362
keywords:
- IRP_MJ_READ union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: d9d98ee9dd106f9edd4cc276cf0d35b3427ad497
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841354"
---
# <a name="flt_parameters-for-irp_mj_read-union"></a>IRP\_MJ\_読み取り共用体の FLT\_パラメーター


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体**で、操作**のブロック構造が[**IRP\_MJ\_READ**](irp-mj-read.md)になっている場合に使用されます。

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

**込ん**  
次のメンバーを含む構造体。

**長さ**  
読み取るデータの長さ (バイト単位)。

**Key**  
ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

**ByteOffset**  
読み取るデータのファイル内のバイトオフセットを開始します。

**ReadBuffer**  
ファイルから読み取られたデータを受け取るバッファーへのポインター。

**MdlAddress**  
**Readbuffer**メンバーが指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_読み取り操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される読み取り操作のパラメーターが含まれています。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_READ は、IRP ベースの操作または高速 i/o 操作にすることができます。

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

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreadfile)

[**IRP\_MJ\_読み取り**](irp-mj-read.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)

 

 






