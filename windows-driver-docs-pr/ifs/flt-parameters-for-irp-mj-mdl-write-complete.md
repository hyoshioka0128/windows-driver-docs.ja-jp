---
title: IRP_MJ_MDL_WRITE_COMPLETE 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造の MajorFunction フィールドが、操作に対する IRP\_MJ\_MDL\_書き込み\_完了したときに使用されます。
ms.assetid: 7b3806fb-b6ba-44f5-88fa-883c7896f0ad
keywords:
- IRP_MJ_MDL_WRITE_COMPLETE union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 7deb556a14f83a53e370ecb9670f0a9ab8e37644
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841370"
---
# <a name="flt_parameters-for-irp_mj_mdl_write_complete-union"></a>IRP\_MJ\_MDL\_書き込み\_完全な共用体の FLT\_パラメーター


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが、操作に対する IRP\_MJ\_MDL\_書き込み\_完了したときに使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER FileOffset;
    PMDL          MdlChain;
  } MdlWriteComplete;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**MdlWriteComplete**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内の開始バイト。

**MdlChain**  
キャッシュされたファイルに書き込まれるデータを含むページを記述する1つ以上のメモリ記述子リスト (MDL) のチェーンへのポインターを受け取る変数へのポインター。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_MDL の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体\_書き込み\_完了操作には、コールバックデータによって表される高速 i/o **MdlWriteComplete**操作のパラメーターが含まれてい[ **\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_MDL\_書き込み\_完了は、高速な i/o 操作です。

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

 

 






