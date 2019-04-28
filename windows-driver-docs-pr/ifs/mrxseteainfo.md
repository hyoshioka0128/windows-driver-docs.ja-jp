---
title: MRxSetEaInfo ルーチン
description: TheMRxSetEaInfo ルーチンは、ネットワークのミニ リダイレクター セットがファイル システム オブジェクトの属性情報を拡張することを要求する RDBSS によって呼び出されます。
ms.assetid: 6882ab3c-a679-491b-a35f-71cfbf77bb39
keywords:
- MRxSetEaInfo ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetEaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbadee5acb93cf4e00be28b4ef2ddcc1626bf3c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382314"
---
# <a name="mrxseteainfo-routine"></a>MRxSetEaInfo ルーチン


*MRxSetEaInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターのセットがファイル システム オブジェクトの属性情報を拡張することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetEaInfo;

NTSTATUS MRxSetEaInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IPR が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxSetEaInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_EA_TOO_LARGE</strong></td>
<td align="left"><p>渡される拡張属性の情報は、リモート共有でサポートされているサイズを超えています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_FILE_CLOSED</strong></td>
<td align="left"><p>SRV_OPEN 構造が閉じられました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワーク アクセスが拒否されました。 このエラーは、ネットワークのミニ リダイレクターが読み取り専用共有上の拡張属性を設定するよう依頼された場合に返されることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモートのページファイルの拡張情報を設定するなど、要求された機能が実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>拡張属性はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクト名が見つかりませんでした。 このエラーは、ネットワーク ミニ リダイレクターが、ファイルの拡張属性を設定するように要求されましたが、ファイルが存在しない場合に返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリーム オブジェクトが渡されたし、リモート ファイル システムがストリームをサポートしていない場合に返されることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>SRV_OPEN 構造が接続されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリック リンクを処理するために、再解析が必要です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxSetEaInfo*受信に応答する[ **IRP\_MJ\_設定\_EA** ](irp-mj-set-ea.md)要求。

呼び出しの前に*MRxSetEaInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryEa.Length**します。

<a name="requirements"></a>必要条件
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

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






