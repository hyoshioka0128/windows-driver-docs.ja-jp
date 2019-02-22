---
title: MRxSetSdInfo ルーチン
description: TheMRxSetSdInfo ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求する RDBSS によって呼び出されます。
ms.assetid: 2a03dde1-440c-4e59-b989-ca4b58b91f3a
keywords:
- MRxSetSdInfo ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetSdInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c09f12d6a10f8f1bb2acf2e258534e1d6bc19c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536366"
---
# <a name="mrxsetsdinfo-routine"></a>MRxSetSdInfo ルーチン


*MRxSetSdInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetSdInfo;

NTSTATUS MRxSetSdInfo(
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

*MRxSetSdInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワーク アクセスが拒否されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>セキュリティ情報リモート ページファイルの設定など、要求された機能が実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>セキュリティ記述子の情報は、リモート共有に対するサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 NTFS ストリーム オブジェクトのセキュリティ情報の設定が要求されたし、リモート ファイル システムがストリームをサポートしていない場合、このエラーを返すことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリック リンクを処理するために、再解析が必要です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxSetSdInfo*受信に応答する[ **IRP\_MJ\_設定\_セキュリティ**](irp-mj-set-security.md)要求。

呼び出しの前に*MRxSetSdInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**SetSecurity.SecurityInformation**に設定されているメンバー **IrpSp -&gt;Parameters.SetSecurity.SecurityInformation**します。

**SetSecurity.SecurityDescriptor**に設定されているメンバー **IrpSp -&gt;Parameters.SetSecurity.SecurityDescriptor**します。

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

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






