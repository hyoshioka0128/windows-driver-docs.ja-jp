---
title: バグ チェック 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
description: THIRD_PARTY_FILE_SYSTEM_FAILURE のバグ チェックでは、0x00000108 の値を持ちます。 これは、サード パーティ製のファイル システムまたはファイル システム フィルターで回復できない問題が発生したことを示します。
ms.assetid: 1ed82617-b0f0-4b41-9af9-b309b6b75dfd
keywords:
- バグ チェック 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
- THIRD_PARTY_FILE_SYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THIRD_PARTY_FILE_SYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c373211e83e83c92bac016c7127312ae5c0e71c2
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521481"
---
# <a name="bug-check-0x108-thirdpartyfilesystemfailure"></a>バグ チェック 0x108:3 番目\_パーティ\_ファイル\_システム\_エラー


3 番目\_パーティ\_ファイル\_システム\_エラーのバグ チェックが 0x00000108 の値を持ちます。 これは、サード パーティ製のファイル システムまたはファイル システム フィルターで回復できない問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="thirdpartyfilesystemfailure-parameters"></a>3 番目\_パーティ\_ファイル\_システム\_エラー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>失敗したファイル システムを識別します。 有効な値は次のとおりです。</p>
<p><strong>1:</strong>Polyserve (Psfs.sys)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>例外レコードのアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>コンテキスト レコードのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの 1 つの考えられる原因は、ディスクの破損です。 サード パーティ製のファイル システムまたはハード ディスク上の不良ブロック (セクター) 内の破損は、このエラーを誘発できます。 破損した SCSI と IDE のドライバーが Windows オペレーティング システムの機能を読み取って、そのため、ディスクに書き込む悪影響を受けることができます、エラーの原因です。

もう 1 つの考えられる原因は、非ページ プール メモリの不足です。 非ページ プールが完全になくなると、このエラーは、システムを停止できます。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

**ディスク破損の問題を解決するには。** デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性があるシステムで、SCSI、IDE、またはその他のディスク コント ローラーからのエラー メッセージをイベント ビューアーを確認します。 ウイルス スキャナー、バックアップ プログラム、またはシステムを継続的に監視するディスク デフラグ ツールを無効にしてください。 ファイル システムまたはファイル システム フィルターの製造元によって提供されるハードウェア診断を実行することも必要があります。

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 これにより、カーネルで使用できる非ページ プール メモリの量が増加します。

 

 




