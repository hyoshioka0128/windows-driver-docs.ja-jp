---
title: IRP_MJ_SET_EA 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、\_MJ\_SET\_EA です。
ms.assetid: 92136272-b40b-4f03-ab31-15184aaccd16
keywords:
- IRP_MJ_SET_EA union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 10d74577bb3c8fc85be1e2b9903e43801b955248
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841348"
---
# <a name="flt_parameters-for-irp_mj_set_ea-union"></a>FLT\_の IRP\_MJ\_設定\_EA 共用体


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、 [ **\_MJ\_SET\_EA**](irp-mj-set-ea.md)です。

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

<a name="members"></a>Members
-------

**SetEa**  
次のメンバーを含む構造体。

**長さ**  
**EaBuffer**が指すバッファーの長さ (バイト単位)。

**EaBuffer**  
呼び出し元によって提供された[**ファイル\_完全\_ea\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)によって設定される拡張属性 (ea) の値を含む入力バッファーを指すポインター。

**MdlAddress**  
**EaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

[**IRP\_MJ\_設定**](irp-mj-set-ea.md)された[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体\_EA 操作には、コールバックデータ ([**FLT\_callback によって表される拡張属性セットのパラメーターが含まれています。\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_SET\_EA は、IRP ベースの操作です。

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


[**ファイル\_EA\_の完全\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IRP\_MJ\_設定\_EA**](irp-mj-set-ea.md)

 

 






