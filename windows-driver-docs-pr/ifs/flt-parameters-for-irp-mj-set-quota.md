---
title: IRP_MJ_SET_QUOTA 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_SET_QUOTA 場合に使用される共用体コンポーネント。
ms.assetid: 4ca19af9-695c-421e-90d5-eb40978f8d19
keywords:
- IRP_MJ_SET_QUOTA ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 26bc8ec147206554e3a9807c66011dda0f1af410
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072241"
---
# <a name="flt_parameters-for-irp_mj_set_quota-union"></a>IRP_MJ_SET_QUOTA 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_SET_QUOTA**](irp-mj-set-quota.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG Length;
    PVOID QuotaBuffer;
    PMDL  MdlAddress;
  } SetQuota;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

**SetQuota**  
次のメンバーを含む構造体。

**長さ**  
**QuotaBuffer**が指すバッファーの長さ (バイト単位)。

**QuotaBuffer**  
設定するクォータ情報を格納する、呼び出し元が指定した[**FILE_QUOTA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)構造化された入力バッファーへのポインター。 このメンバーは省略可能であり、MDL が**Mdladdress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**QuotaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **QuotaBuffer**でバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>コメント

[**IRP_MJ_SET_QUOTA**](irp-mj-set-quota.md)操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される、設定-クォータ情報操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

**QuotaBuffer**と**mdladdress**の両方のバッファーを指定する場合は、ミニフィルターを使用することをお勧めします。 **QuotaBuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

IRP_MJ_SET_QUOTA は、IRP ベースの操作です。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| ヘッダー | Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>参照

[**FILE_QUOTA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IRP_MJ_SET_QUOTA**](irp-mj-set-quota.md)
