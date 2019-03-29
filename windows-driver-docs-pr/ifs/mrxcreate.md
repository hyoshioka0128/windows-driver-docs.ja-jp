---
title: MRxCreate ルーチン
description: TheMRxCreate ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトを作成することを要求する RDBSS によって呼び出されます。
ms.assetid: d1b664cf-37b6-4c65-8634-21695af2db21
keywords:
- MRxCreate ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxCreate
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddbd534db0b801ba91190115e3bf010af23f8962
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349465"
---
# <a name="mrxcreate-routine"></a>MRxCreate ルーチン


*MRxCreate*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトを作成することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCreate;

NTSTATUS MRxCreate(
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

*MRxCreate*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>操作を完了するリソースの不足が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワーク アクセスが拒否されました。 このエラーは、ネットワーク ミニ リダイレクターが読み取り専用共有で新しいファイルを開くよう依頼された場合に返されることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモート ブートまたはリモートのページファイルなど、要求された機能が実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>拡張属性など、要求された機能がサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_COLLISION</strong></td>
<td align="left"><p>ネットワークのミニ リダイレクターは、既に存在するファイルを作成するように要求されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクト名が見つかりませんでした。 このエラーは、ネットワーク ミニリダイレクターが存在しないファイルを開くよう依頼された場合に返されることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリーム オブジェクトを要求し、リモート ファイル システムがストリームをサポートしていない場合に返されることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリック リンクを処理するために、再解析が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_RETRY</strong></td>
<td align="left"><p>操作を再試行する必要があります。 このエラーは、ネットワークのミニ リダイレクターは、共有違反や、アクセス拒否エラーが発生しました。 場合に返されることができます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

*MRxCreate*はネットワークのミニ リダイレクターがネットワーク経由でファイル システム オブジェクトを開くことを要求する RDBSS によって呼び出されます。 この呼び出しが受信する応答 RDBSS によって発行された、 [ **IRP\_MJ\_作成**](irp-mj-create.md)要求。

呼び出しの前に*MRxCreate*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**pRelevantSrvOpen** 、SRV に設定されている\_オープン構造体。

**Create.pSrvCall** 、SRV に設定されている\_呼び出し構造体。

**Create.NtCreateParameters**要求 NT に設定されている\_作成\_パラメーター。

ネットワークのミニ リダイレクターのコンテキストでは、ファイル オブジェクトは、ファイル オブジェクトの拡張機能 (FOBX) 構造体と関連付けられているファイル制御ブロック (FCB) を参照します。 ファイル オブジェクトと FOBXs、一対一で対応があります。 多くのファイル オブジェクトは、リモート サーバー上の 1 つのファイルを表す同じの FCB を参照してください。 クライアントが同じ FCB のいくつかの異なるオープン要求 (NtCreateFile 要求) を持つことができ、これらの新しいファイル オブジェクトが作成されます。 少ない送信 RDBSS とネットワークのミニ リダイレクターできます*MRxCreate* 、SRV の有効な共有 NtCreateFile 要求受信されるよりも要求\_オープン構造体をいくつか FOBXs。

場合、 *MRxCreate*ファイルの上書きの要求でしたと*MRxCreate*状態が返されました\_成功すると、し RDBSS はページング I/O リソースが取得されて、ファイルを切り捨てます。 ファイルは、キャッシュ マネージャーによってキャッシュされているが、RDBSS により、キャッシュ マネージャーがだけのものでのサーバーから受信した、サイズが更新されます。

、戻る前に*MRxCreate*設定する必要があります、 **CurrentIrp -&gt;IoStatus.Information** 、RX のメンバー\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

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


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






