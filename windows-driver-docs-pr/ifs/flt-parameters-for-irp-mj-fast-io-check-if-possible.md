---
title: IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造の MajorFunction フィールドが IRP\_MJ\_高速\_IO\_\_可能な場合に使用されます。
ms.assetid: 1de62b03-4073-40d6-9094-609431e19e5b
keywords:
- IRP_MJ_FAST_IO_CHECK_IF_POSSIBLE union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: f3200d6f0e6e038e030a14a1b61ad3b4727d93a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841382"
---
# <a name="flt_parameters-for-irp_mj_fast_io_check_if_possible-union"></a>FLT\_の IRP\_MJ\_高速\_IO\_IF union が可能な場合\_チェック\_


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが、操作に対する IRP\_MJ\_高速\_IO\_の場合に使用され\_得る.

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER             FileOffset;
    ULONG                     Length;
    ULONG POINTER_ALIGNMENT   LockKey;
    BOOLEAN POINTER_ALIGNMENT CheckForReadOperation;
  } FastIoCheckIfPossible;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**可能な場合**  
次のメンバーを含む構造体。

**FileOffset**  
キャッシュされたファイル内の開始バイトオフセット。

**長さ**  
読み取りまたは書き込みを行うデータの長さ (バイト単位)。

**LockKey**  
ターゲットファイルのバイト範囲ロックに関連付けられたキー値。 読み取りまたは書き込みを行う範囲がファイル内の排他的にロックされている範囲の場合、このパラメーターはその共有ロックのキーである必要があります。 共有ロックは、呼び出し元のスレッドの親プロセスによって保持されている必要があります。それ以外の場合、このパラメーターは無視されます。

**CheckForReadOperation**  
この操作で読み取りまたは書き込み操作を確認するかどうかを指定します。 読み取り操作の場合は**TRUE**に、書き込み操作の場合は**FALSE**に設定されます。

<a name="remarks"></a>注釈
-------

IRP\_MJ の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体\_高速\_IO\_チェック\_(可能な操作\_に、コールバックによって表される迅速**な操作の**パラメーターが含まれている場合)データ ([**FLT\_CALLBACK\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_高速\_IO\_チェック\_可能であれば高速な i/o 操作であることを確認します。

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

[**FsRtlAreThereCurrentFileLocks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlaretherecurrentfilelocks)

[**FsRtlCopyRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopyread)

[**FsRtlCopyWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcopywrite)

 

 






