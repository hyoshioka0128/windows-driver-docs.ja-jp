---
title: IRP_MJ_QUERY_QUOTA 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_QUERY_QUOTA 場合に使用される共用体コンポーネント。
ms.assetid: b87b008d-f1ce-4dab-9afa-df67aa3dc596
keywords:
- IRP_MJ_QUERY_QUOTA ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 3789658e4b68e12fccbb350305587fa3fb27fb64
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968325"
---
# <a name="flt_parameters-for-irp_mj_query_quota-union"></a>IRP_MJ_QUERY_QUOTA 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                       Length;
    PSID                        StartSid;
    PFILE_GET_QUOTA_INFORMATION SidList;
    ULONG                       SidListLength;
    PVOID                       QuotaBuffer;
    PMLD                        MdlAddress;
  } QueryQuota;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>メンバー

**QueryQuota**  
次のメンバーを含む構造体。

**[データ型]**  
**QuotaBuffer**が指すバッファーの長さ (バイト単位)。

**StartSid**  
クォータ一覧のスキャンを開始するエントリのセキュリティ識別子 (SID) へのポインター (省略可能)。 操作の FLT_IO_PARAMETER_BLOCK 構造体に SL_INDEX_SPECIFIED フラグが設定されていない場合、または**Sidlist**が空でないリストを指している場合、このパラメーターは無視されます。

**SidList**  
クォータ情報を照会する Sid を指定する、呼び出し元が指定した FILE_GET_QUOTA_INFORMATION 構造化入力バッファーへのポインター。

**SidListLength**  
**Sidlist**が指すバッファーの長さ (バイト単位)。

**QuotaBuffer**  
クォータ情報が返される、呼び出し元が指定した[**FILE_QUOTA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)構造化された出力バッファーへのポインター。 このメンバーは省略可能であり、MDL が**Mdladdress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**QuotaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **QuotaBuffer**でバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>注釈

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される、IRP ベースのクエリのクォータ情報操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

**QuotaBuffer**と**mdladdress**の両方のバッファーを指定する場合は、ミニフィルターを使用することをお勧めします。 **QuotaBuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

IRP_MJ_QUERY_QUOTA は、IRP ベースの操作です。

## <a name="requirements"></a>要件

**ヘッダー**: fltkernel .H (fltkernel .h を含む)


## <a name="see-also"></a>関連項目

[**FILE_QUOTA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)
