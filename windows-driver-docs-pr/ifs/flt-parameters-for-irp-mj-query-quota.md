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
ms.openlocfilehash: 276622c2e08332d08edf16d759371a717fc528a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361923"
---
# <a name="fltparameters-for-irpmjqueryquota-union"></a>FLT\_IRP のパラメーター\_MJ\_クエリ\_クォータ共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)します。

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

<a name="members"></a>メンバー
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
呼び出し元が指定へのポインター [**ファイル\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540342)-クォータ情報が返される構造化した出力バッファー。

**MdlAddress**  
バッファーを記述するメモリ記述子一覧 (MDL) のアドレスを**QuotaBuffer**を指します。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)操作にコールバック データによって表される IRP ベース クォータ情報の照会操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620))構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_クエリ\_クォータは IRP ベースの操作。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_クォータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540342)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IoCheckQuotaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548279)

[**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)

[**SID**](https://msdn.microsoft.com/library/windows/hardware/ff556740)

 

 






