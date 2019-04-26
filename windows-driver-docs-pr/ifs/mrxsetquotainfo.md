---
title: MRxSetQuotaInfo ルーチン
description: TheMRxSetQuotaInfo ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求する RDBSS によって呼び出されます。
ms.assetid: 43d8669f-d122-4385-87a3-bf31bac9dfd2
keywords:
- MRxSetQuotaInfo ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetQuotaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ab64a3b59b7aff11d306011eb34e199b25f80b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352842"
---
# <a name="mrxsetquotainfo-routine"></a>MRxSetQuotaInfo ルーチン


*MRxSetQuotaInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetQuotaInfo;

NTSTATUS MRxSetQuotaInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxSetQuotaInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>呼び出し元には、この操作に適切なセキュリティが不足していました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>クォータはサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxSetQuotaInfo*受信に応答する[ **IRP\_MJ\_設定\_クォータ**](irp-mj-set-quota.md)要求。

呼び出しの前に*MRxSetQuotaInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

*Info.Buffer*メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.SetQuota.Length**します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






