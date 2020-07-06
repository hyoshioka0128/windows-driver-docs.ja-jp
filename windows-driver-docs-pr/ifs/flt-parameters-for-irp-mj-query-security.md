---
title: IRP_MJ_QUERY_SECURITY 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_QUERY_SECURITY 場合に使用される共用体コンポーネント。
ms.assetid: 7707fec2-9fe8-40f6-9f34-f43403551440
keywords:
- IRP_MJ_QUERY_SECURITY ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 57dbbfb21b8a333d331e3e318333ba5af4981d02
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968321"
---
# <a name="flt_parameters-for-irp_mj_query_security-union"></a>IRP_MJ_QUERY_SECURITY 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION    SecurityInformation;
    ULONG POINTER_ALIGNMENT Length;
    PVOID                   SecurityBuffer;
    PDML                    MdlAddress;
  } QuerySecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>メンバー

**QuerySecurity**  
次のメンバーを含む構造体。

**SecurityInformation**  
照会するセキュリティ情報を指定する、呼び出し元から提供された[**SECURITY_INFORMATION**](security-information.md)値へのポインター。 次のいずれか:

| SecurityInformation の値 | 説明 |
| ------------------------- | ------- |
| OWNER_SECURITY_INFORMATION | オブジェクトの所有者識別子が照会されています。 READ_CONTROL アクセスが必要です。 |
| GROUP_SECURITY_INFORMATION | オブジェクトのプライマリグループ識別子が照会されています。 READ_CONTROL アクセスが必要です。 |
| DACL_SECURITY_INFORMATION | オブジェクトの随意アクセス制御リスト (DACL) を照会しています。 READ_CONTROL アクセスが必要です。 |
| SACL_SECURITY_INFORMATION | オブジェクトのシステム ACL (SACL) を照会しています。 ACCESS_SYSTEM_SECURITY アクセスが必要です。 |

**[データ型]**  
**Securitybuffer**が指すバッファーの長さ (バイト単位)。

**SecurityBuffer**  
指定したオブジェクトのセキュリティ記述子のコピーを受け取る、呼び出し元から提供される出力バッファーへのポインター。 呼び出しプロセスには、オブジェクトのセキュリティステータスの指定した側面を表示する権限が必要です。 [**SECURITY_DESCRIPTOR**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))構造体は、自己相対形式で返されます。 このメンバーは省略可能であり、MDL が**Mdladdress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**Securitybuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **securitybuffer**にバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>注釈

[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される、IRP ベースのクエリセキュリティ情報操作のパラメーターが含まれています。 これは[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

**Securitybuffer**と**mdladdress**バッファーの両方が指定されている場合は、ミニフィルターで MDL を使用することをお勧めします。 **Securitybuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

Windows XP 以降では、FLT_IO_PARAMETER_BLOCK 構造体の**Targetfileobject**メンバーが指すオブジェクトは、名前付きデータストリームを表すことができます。 名前付きデータストリームの詳細については、「 [**FILE_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)」を参照してください。

IRP_MJ_QUERY_SECURITY は、IRP ベースの操作です。

## <a name="requirements"></a>要件

**ヘッダー**: fltkernel .H (fltkernel .h を含む)


## <a name="see-also"></a>関連項目

[**FILE_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)

[**SECURITY_DESCRIPTOR**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**SECURITY_INFORMATION**](security-information.md)
