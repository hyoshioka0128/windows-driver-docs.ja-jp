---
title: IRP_MJ_MDL_READ 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーターの\_ブロック構造体の MJ が IRP\_\_MDL\_READ である場合に使用されます。
ms.assetid: d07d3ba2-a405-481c-986b-7e26cda61909
keywords:
- IRP_MJ_MDL_READ union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 18f766d47238a1414525b6d34518dd8e3e01468a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841372"
---
# <a name="flt_parameters-for-irp_mj_mdl_read-union"></a>IRP\_MJ\_MDL\_読み取り共用体の FLT\_パラメーター


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーターの\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の MJ が IRP\_\_MDL\_READ**である場合**に使用されます。

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
キャッシュされたファイル内の開始バイト。

**長さ**  
キャッシュされたファイルから読み取るデータの長さ (バイト単位)。

**Key**  
ターゲットファイルのバイト範囲ロックに関連付けられたキー値。 読み取り対象の範囲がファイル内で排他的にロックされている範囲と重複している場合、このパラメーターはその排他ロックのキーである必要があります。 排他ロックは、呼び出し元のスレッドの親プロセスによって保持されている必要があります。それ以外の場合、このパラメーターは無視されます。

**MdlChain**  
読み取るデータを含むページを記述する1つ以上のメモリ記述子リスト (MDL) のチェーンへのポインターを受け取る変数へのポインター。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_MDL\_読み取り操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) によって表される高速 i/o **mdlread**操作のパラメーターが含まれています。データ. これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

高速 i/o IRP\_MJ\_MDL\_読み取り要求が失敗した場合、i/o の発行者によって、要求を再発行する方法が決まります。 ミニフィルターでは、必ずしも IRP ベースの IRP\_MJ\_MDL\_読み取ることはできません。 たとえば、irp 要求は、IRP\_MJ\_READ/IRP\_\_MDL として再発行される可能性があります。

IRP\_MJ\_MDL\_READ は、高速な i/o 操作です。

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

 

 






