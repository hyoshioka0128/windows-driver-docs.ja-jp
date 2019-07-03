---
title: バグ チェック 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
description: KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION のバグ チェックでは、0x00000153 の値を持ちます。 これは、スレッドがその AutoBoost ロック エントリを解放した前に終了したことを示します。
ms.assetid: 0837C084-DAB8-4064-903D-10CD5CDE65E5
keywords:
- バグ チェック 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf418808a92609b1a6f79646b9979cf90595d466
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520057"
---
# <a name="bug-check-0x153-kernellockentryleakedonthreadtermination"></a>バグ チェック 0x153:カーネル\_ロック\_エントリ\_漏洩した\_ON\_スレッド\_終了


カーネル\_ロック\_エントリ\_漏洩した\_ON\_スレッド\_終了バグ チェックが 0x00000153 の値を持ちます。 これは、スレッドがその AutoBoost ロック エントリを解放した前に終了したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="kernellockentryleakedonthreadtermination-parameters"></a>カーネル\_ロック\_エントリ\_漏洩した\_ON\_スレッド\_終了パラメーター


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
<td align="left">スレッドのアドレス</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">解放されていないエントリのアドレス</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>エントリの状態を示す状態コード</p>
<p>0x1:ロックのポインターが NULL でした。</p>
<p>0x2:スレッドのポインターが予約されているビットが設定されました。</p>
<p>0x3:スレッドのポインターが破損しています</p>
<p>0x4:エントリが未解決の IO や CPU のブーストが左</p></td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

これは通常、スレッドに (例: 別のスレッドを解放することで証明書利用者) で以前に取得したロックが解放されない場合、またはスレッドが一貫性のある一連のパッケージ Api をロックするフラグを指定しなかった場合に発生します。

 

 




