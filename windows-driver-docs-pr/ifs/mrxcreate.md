---
title: MRxCreate ルーチン
description: TheMRxCreate ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトを作成するように要求するために、RDBSS によって呼び出されます。
ms.assetid: d1b664cf-37b6-4c65-8634-21695af2db21
keywords:
- MRxCreate ルーチンのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 388b2c2517d02e8906549e7469268a2f79e54984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841115"
---
# <a name="mrxcreate-routine"></a>MRxCreate ルーチン


*MRxCreate*ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトを作成するように要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCreate;

NTSTATUS MRxCreate(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxCreate*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>操作を完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワークアクセスが拒否されました。 このエラーは、ネットワークミニリダイレクターが読み取り専用の共有で新しいファイルを開くように要求された場合に返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモートブートやリモートページファイルなど、要求された機能は実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>拡張属性など、要求された機能はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_COLLISION</strong></td>
<td align="left"><p>ネットワークミニリダイレクターは、既に存在するファイルを作成するように求められました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクト名が見つかりませんでした。 このエラーは、ネットワークミニリダイレクターが、存在しないファイルを開くように要求された場合に返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリームオブジェクトが要求され、リモートファイルシステムでストリームがサポートされていない場合に返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリックリンクを処理するには、再解析が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_RETRY</strong></td>
<td align="left"><p>操作を再試行する必要があります。 ネットワークミニリダイレクターで共有違反またはアクセス拒否エラーが発生した場合、このエラーが返されることがあります。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

*MRxCreate*は、ネットワーク上でファイルシステムオブジェクトを開くようにネットワークミニリダイレクターに要求するために、RDBSS によって呼び出されます。 この呼び出しは、 [**IRP\_MJ\_CREATE**](irp-mj-create.md)要求の受信に応答して、RDBSS によって発行されます。

*MRxCreate*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**pRelevantSrvOpen**は、オープン構造の SRV\_に設定されます。

**Create. pSrvCall**は SRV\_呼び出し構造に設定されます。

**作成します。 NtCreateParameters**は、要求された NT\_作成\_パラメーターに設定されます。

ネットワークミニリダイレクターのコンテキストでは、ファイルオブジェクトは、関連付けられたファイルコントロールブロック (FCB) とファイルオブジェクト拡張 (FOBX) 構造体を参照します。 ファイルオブジェクトと FOBXs の間には1対1の対応があります。 多くのファイルオブジェクトは、リモートサーバー上の1つのファイルを表す同じ FCB を参照します。 クライアントは、同じ FCB で複数の異なる open requests (NtCreateFile requests) を持つことができ、これらはそれぞれ新しいファイルオブジェクトを作成します。 RDBSS とネットワークミニリダイレクターは、受信した NtCreateFile 要求よりも*MRxCreate*要求を送信することを選択できます。これは、SRV\_オープン構造体を複数の FOBXs 間で共有する場合に有効です。

*MRxCreate*要求がファイルの上書き用であり、 *MRxCreate*が状態\_SUCCESS を返した場合、RDBSS はページング i/o リソースを取得し、ファイルを切り詰めます。 ファイルがキャッシュマネージャーによってキャッシュされている場合、RDBSS は、サーバーから受け取ったものと共に、キャッシュマネージャーが持つサイズを更新します。

MRxCreate を返す前に、 *RxContext*パラメーターによって示される RX\_コンテキスト構造のメンバーを **&gt;** 設定する必要があります。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






