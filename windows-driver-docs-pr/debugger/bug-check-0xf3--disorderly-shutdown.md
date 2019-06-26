---
title: バグ チェック 0xF3 DISORDERLY_SHUTDOWN
description: DISORDERLY_SHUTDOWN のバグ チェックでは、0x000000F3 の値を持ちます。 これは、Windows がメモリ不足のためにシャット ダウンにできなかったことを示します。
ms.assetid: e113cd2f-96b2-43b8-a67e-a851cc5c0da8
keywords:
- バグ チェック 0xF3 DISORDERLY_SHUTDOWN
- DISORDERLY_SHUTDOWN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DISORDERLY_SHUTDOWN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2b77205e391b9e36935e8bd05249d21e8c20400
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361502"
---
# <a name="bug-check-0xf3-disorderlyshutdown"></a>バグ チェック 0xF3:無秩序\_シャット ダウン


DISORDERLY\_シャット ダウンのバグ チェックが 0x000000F3 の値を持ちます。 これは、Windows がメモリ不足のためにシャット ダウンにできなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="disorderlyshutdown-parameters"></a>無秩序\_-SHUTDOWN パラメーター


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
<td align="left"><p>ダーティ ページの合計数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ページファイル宛てのダーティ ページの数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Windows Server 2003 ののみ:ページ単位でのバグ チェック時に使用可能な非ページ プールのサイズ</p>
<p>Windows Vista 以降。予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Windows Server 2003 ののみ:現在のステージをシャット ダウン</p>
<p>Windows Vista 以降。最新の変更の書き込みエラーの状態</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

シャット ダウン、Windows が継続的に使用可能な空きページがありませんでした。

アプリケーションが終了していないドライバーがアンロードされていなかったため、変更ライターが終了した後にもページにアクセスする、続行します。 これにより、ページのファイルに使用される可能性がありますページ不足、実行するシステムです。

 

 




