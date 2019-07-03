---
title: バグ チェック 0x103 MUP_FILE_SYSTEM
description: MUP_FILE_SYSTEM のバグ チェックでは、0x00000103 の値を持ちます。
ms.assetid: 2756bdcc-5b10-481e-99ec-17b00c4f459d
keywords:
- バグ チェック 0x103 MUP_FILE_SYSTEM
- MUP_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUP_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 21184e1db60bcefefcc4cdd3fee816724fe81584
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521586"
---
# <a name="bug-check-0x103-mupfilesystem"></a>バグ チェック 0x103:MUP\_ファイル\_システム


MUP\_ファイル\_システムのバグ チェックが 0x00000103 の値を持ちます。 このバグ チェックでは、複数 UNC プロバイダー (MUP) が無効または予期しないデータを発生したことを示します。 結果として、MUP はネットワーク リダイレクター、汎用名前付け規則 (UNC) プロバイダーをリモート ファイル システムの要求をチャネルすることはできません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="mupfilesystem-parameters"></a>MUP\_ファイル\_システム パラメーター


パラメーター 1 では、違反の種類を識別します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>保留中の IRP のアドレス。</p></td>
<td align="left"><p>コンテキストを持つファイルが見つかりませんでした。 ファイル オブジェクトのアドレス。</p></td>
<td align="left"><p>デバイス オブジェクトのアドレス。</p></td>
<td align="left"><p>MUP は、ファイル オブジェクトに対応するファイルのコンテキストが見つかりませんでした。 これは、通常、MUP MUP が対応する irp_mj_create 用要求に見当たらないファイル オブジェクトの I/O 要求が多いことを示します。 このバグ チェックの可能性の高い原因は、フィルター ドライバー エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>予想されるファイルのコンテキストのアドレス。</p></td>
<td align="left"><p>実際には、ファイル オブジェクトから取得されたアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ファイル コンテキストが、ファイル オブジェクトの存在しているだけで、想定されたされませんが (たとえば、ことが考えられます<strong>NULL</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>IRP コンテキストのアドレス。</p></td>
<td align="left"><p>IRP の完了ステータス コード。</p></td>
<td align="left"><p>IRP の完了した UNC プロバイダーのドライバー オブジェクト (あります<strong>NULL</strong>)。</p></td>
<td align="left"><p>IRP の完了状態は予期されない、または無効でした。</p>
<p>このバグ チェックでは、レガシ ネットワーク リダイレクターに接続されているファイル システム フィルター ドライバーによってのみ発生する必要があり、チェック ビルドの Windows を使用している場合にのみ発生します。 レガシ リダイレクターを使用して、 <strong>FsRtlRegisterUncProvider</strong> MUP に登録します。 このバグ チェックでは、フィルター ドライバー、NTSTATUS IRP_MJ_CLEANUP または未完了の要求ではない STATUS_SUCCESS を返すことを検出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>IRP のアドレス</p></td>
<td align="left"><p>ファイル オブジェクトのアドレス</p></td>
<td align="left"><p>ファイル オブジェクトのファイル コンテキスト</p></td>
<td align="left"><p>ファイル オブジェクトの作成要求が完了する前に、ファイル オブジェクトの I/O 操作が開始されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

MUP では、処理のすべてのファイル オブジェクトのファイル オブジェクトごとにコンテキスト情報を保持します。

 

 




