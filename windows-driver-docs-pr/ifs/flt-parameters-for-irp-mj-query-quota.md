---
title: FLT_PARAMETERS IRP_MJ_QUERY_QUOTA 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_クエリ\_クォータ。
ms.assetid: b87b008d-f1ce-4dab-9afa-df67aa3dc596
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_QUOTA 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 6b0eb58dabe3b94dbdd7bd5bb86c81fcc3f891e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383400"
---
# <a name="fltparameters-for-irpmjqueryquota-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_クォータ共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)します。

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
バッファーのバイト単位の長さを**QuotaBuffer**を指します。

**StartSid**  
省略可能なポインターのセキュリティにクォータ リストをスキャンを開始する位置にあるエントリの識別子 (SID)。 場合、このパラメーターは無視されます、SL\_インデックス\_、FLT で指定したフラグが設定されていない\_IO\_パラメーター\_操作のブロック構造または**してください**ポイント空でないリスト。

**してください。**  
呼び出し元が指定したファイルへのポインター\_取得\_クォータ\_情報構造のクォータ情報がクエリを実行できますが、Sid を指定する入力バッファー。

**SidListLength**  
バッファーのバイト単位の長さを**してください**を指します。

**QuotaBuffer**  
呼び出し元が指定へのポインター [**ファイル\_クォータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_quota_information)-クォータ情報が返される構造化した出力バッファー。

**MdlAddress**  
バッファーを記述するメモリ記述子一覧 (MDL) のアドレスを**QuotaBuffer**を指します。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)の構造体[ **IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)操作にコールバック データによって表される IRP ベース クォータ情報の照会操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data))構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_クォータは IRP ベースの操作。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_クォータ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_quota_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckQuotaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_sid)

 

 






