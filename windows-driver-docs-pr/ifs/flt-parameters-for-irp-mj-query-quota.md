---
title: IRP_MJ_QUERY_QUOTA 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーター\_操作のブロック構造の MajorFunction フィールドが IRP\_MJ\_クエリ\_クォータである場合に使用される共用体コンポーネント。
ms.assetid: b87b008d-f1ce-4dab-9afa-df67aa3dc596
keywords:
- IRP_MJ_QUERY_QUOTA union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: fa2c35f28f6b782edaf8aa127ddcfd0c5ba27a54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841360"
---
# <a name="flt_parameters-for-irp_mj_query_quota-union"></a>IRP\_MJ の FLT\_パラメーター\_クエリ\_クォータ共用体


[**FLT\_IO\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作のブロック構造の**MajorFunction**フィールドが[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)である場合に使用される共用体コンポーネント。

<a name="syntax"></a>構文
------

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

<a name="members"></a>Members
-------

**QueryQuota**  
次のメンバーを含む構造体。

**長さ**  
**QuotaBuffer**が指すバッファーの長さ (バイト単位)。

**StartSid**  
クォータ一覧のスキャンを開始するエントリのセキュリティ識別子 (SID) へのポインター (省略可能)。 このパラメーターは、SL\_インデックス\_指定されたフラグが、操作の FLT\_IO\_パラメーター\_ブロック構造で設定されていない場合、または**Sidlist**が空でないリストを指している場合には無視されます。

**SidList**  
呼び出し元が指定したファイルへのポインター\_\_クォータ情報を取得し、クォータ情報を照会する Sid を指定する\_情報を構造化した入力バッファーを取得します。

**SidListLength**  
**Sidlist**が指すバッファーの長さ (バイト単位)。

**QuotaBuffer**  
呼び出し元が指定したファイルへのポインター [ **\_クォータの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)によって、クォータ情報が返される場所を指定します。

**MdlAddress**  
**QuotaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

[**Irp\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータで表される irp ベースのクエリのクォータ情報操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_クエリ\_クォータは、IRP ベースの操作です。

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


[**ファイル\_クォータの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

 

 






