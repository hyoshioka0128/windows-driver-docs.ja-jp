---
title: バグ チェック 0x143 PROCESSOR_DRIVER_INTERNAL
description: PROCESSOR_DRIVER_INTERNAL のバグ チェックでは、0x00000143 の値を持ちます。 これは、プロセッサの電源管理 (PPM) ドライバーに致命的なエラーが発生したことを示します。
ms.assetid: B61A1DF1-4454-4418-866F-FD9EC96F6906
keywords:
- バグ チェック 0x143 PROCESSOR_DRIVER_INTERNAL
- PROCESSOR_DRIVER_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PROCESSOR_DRIVER_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1766f98e3ba794c439ab187d494a7719e8525ea7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903010"
---
# <a name="bug-check-0x143-processordriverinternal"></a>バグ チェック 0x143:プロセッサ\_ドライバー\_内部


プロセッサ\_ドライバー\_内部バグ チェックが 0x00000143 の値を持ちます。 これは、プロセッサの電源管理 (PPM) ドライバーに致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="processordriverinternal-parameters"></a>プロセッサ\_ドライバー\_内部パラメーター


| パラメーター | 説明                                                              |
|-----------|--------------------------------------------------------------------------|
| 1         | 1-power エンジン Plugin(PEP) が必要な通知を受理できませんでした。    |
| 2         | PEP ランタイム通知の種類                                            |
| 3         | 通知メッセージへのポインター                                          |
| 4         | プロセッサのデバイス コンテキストへのポインター (FDO\_データ)、通知の発行 |

 

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
<td align="left">1</td>
<td align="left">2-power エンジン プラグイン (PEP) に無効なプロセッサのアイドル状態が返されます</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>無効な状態の種類</p>
<p>0x0 :PEP 要求調整のアイドル状態のプロセッサが多すぎます。</p>
パラメーター 3 - プロセッサの数の要求プロセッサ デバイス コンテキスト (FDO_DATA) へのポインターをアイドル状態の遷移パラメーター 4 - 調整に参加するには
<p>0x1:PEP に無効なアイドル状態で要求されたプロセッサ</p>
パラメーター 3 - アイドル状態のインデックスが要求されたパラメーター 4 - 無効なアイドル状態に対応するプロセッサ デバイス コンテキスト (FDO_DATA) へのポインター
<p>0x2:PEP 要求が無効なアイドル状態にするプラットフォーム</p>
パラメーター 3 - プラットフォームのアイドル状態のインデックスが要求されたパラメーター 4 - 無効なアイドル状態に対応するプロセッサ デバイス コンテキスト (FDO_DATA) へのポインター</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

プロセッサのドライバーには、バグチェックを求めるメッセージが表示される状態の条件が検出されました。 プロセッサのアイドル時にこのような可能性がありますし、パフォーマンス状態の変更の実行は、このようなその他のエンティティに関連する可能性がありますがカーネル、HAL および電源エンジン プラグイン (PEP) します。 バグチェックからの情報は、特定の他のエンティティを処理するプロセッサのドライバーの仮定に違反していたのに役立ちます。 根本原因が他のエンティティである可能性があり、ダンプ ファイルがバグチェックの理由を確認する方法の詳細を表示可能性があります。

 

 




