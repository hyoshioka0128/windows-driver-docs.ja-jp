---
title: IRP_MJ_QUERY_EA 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、IRP\_MJ\_QUERY\_EA です。
ms.assetid: 858e8c72-33ae-441c-ada9-86c5df0e4f59
keywords:
- IRP_MJ_QUERY_EA ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- PFLT_PARAMETERS 共用体ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: e5e658237b121537b4b3590d3b0316e0f7a385cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841380"
---
# <a name="flt_parameters-for-irp_mj_query_ea-union"></a>IRP\_MJ の FLT\_パラメーター\_クエリ\_EA 共用体


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネントは、 [**IRP\_MJ\_QUERY\_EA**](irp-mj-query-ea.md)です。

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

**Quer**  
次のメンバーを含む構造体。

**長さ**  
**EaBuffer**が指すバッファーの長さ (バイト単位)。

**EaList**  
呼び出し元によって提供されたファイルへのポインター。\_EA\_情報構造化入力バッファーを取得し、クエリ対象の拡張属性を指定します。\_ます。

**EaListLength**  
**Ealist**が指すバッファーの長さ (バイト単位)。

**Eライド Dex**  
拡張属性リストのスキャンを開始する位置のエントリのインデックス。 このパラメーターは、SL\_インデックス\_指定されたフラグが、操作の FLT\_IO\_パラメーター\_ブロック構造で設定されていない場合、または**Ealist**が空でないリストを指している場合には無視されます。

**EaBuffer**  
呼び出し元から提供された[**ファイル\_完全\_EA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)拡張属性値が返される場所を指すポインター。

**MdlAddress**  
**EaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

[**Irp\_MJ\_QUERY\_EA**](irp-mj-query-ea.md)操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造によって表される、irp ベースのクエリ拡張属性情報操作のパラメーターが含まれています。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_クエリ\_EA は、IRP ベースの操作です。

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

[**IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)

 

 






