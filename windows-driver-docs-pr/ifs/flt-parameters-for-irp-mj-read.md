---
title: IRP_MJ_READ 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_READ 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: 48674db7-c0cc-45a0-bce9-eaf1a4cec362
keywords:
- IRP_MJ_READ ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 753ba62acf5e4639c7e47a25ba79d72018b60726
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072229"
---
# <a name="flt_parameters-for-irp_mj_read-union"></a>IRP_MJ_READ 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_READ**](irp-mj-read.md)場合は、次の共用体コンポーネントが使用されます。

## <a name="syntax"></a>構文

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

## <a name="members"></a>Members

**込ん**  
次のメンバーを含む構造体。

**長さ**  
読み取るデータの長さ (バイト単位)。

**キー**  
ターゲットファイルのバイト範囲ロックに関連付けられたキー値。

**ByteOffset**  
読み取るデータのファイル内のバイトオフセットを開始します。

**ReadBuffer**  
ファイルから読み取られたデータを受け取るバッファーへのポインター。 このメンバーは省略可能であり、MDL が**Mdladdress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**Readbuffer**メンバーが指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **Readbuffer**にバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>コメント

IRP_MJ_READ 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される読み取り操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

**Readbuffer**と**mdladdress**バッファーの両方が指定されている場合は、ミニフィルターで MDL を使用することをお勧めします。 **Readbuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

IRP_MJ_READ は、IRP ベースの操作でも、高速な i/o 操作でもかまいません。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| ヘッダー | Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>参照

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreadfile)

[**IRP_MJ_READ**](irp-mj-read.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)
