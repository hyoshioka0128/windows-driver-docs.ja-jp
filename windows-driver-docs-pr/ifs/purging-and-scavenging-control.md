---
title: 消去と清掃の制御
description: 消去と清掃の制御
ms.assetid: 103b05e6-333a-441a-a4f8-784ae43df59e
keywords:
- RDBSS WDK ファイル システムでは、消去し、構造体の清掃を行う
- リダイレクトされたバッファリング サブシステム WDK のドライブのファイル システムでは、消去し、構造体の清掃を行う
- WDK ネットワーク リダイレクターの消去
- 清掃の WDK ネットワーク リダイレクター
- FOBX 構造体
- クリーンアップ FOBX 構造 WDK ネットワーク リダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4669709474c913c6b13bb4786c60d5744c72739
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370125"
---
# <a name="purging-and-scavenging-control"></a>消去と清掃の制御


## <span id="ddk_purging_and_scavenging_control_if"></span><span id="DDK_PURGING_AND_SCAVENGING_CONTROL_IF"></span>


RDBSS 数を消去し、不要になったとき FOBX 構造体の清掃を行うルーチンを提供します。

クリーンアップでは、ファイル オブジェクトに関連付けられた複数ユーザー ハンドルのないです。 このような場合は、閉じてクリーンアップ間の時間枠は、メモリ マネージャーおよびキャッシュ マネージャーによって管理されるその他の参照によって決まります。 RDBSS 清掃を行うし、不要な FOBX、およびその他の構造を消去する別のスレッドで実行されているスカベン ジャー プロセスを使用します。

現時点では、清掃は実装されて SRV\_呼び出し、NET\_ルートと V\_NET\_ルート構造体。 FCB の清掃が個別に処理されます。 FOBX でき、同期的に完了する必要がありますは常にします。 清掃の終了処理を有効にする可能性がある必要がある唯一のデータ構造は SRV\_オープン構造体。

スカベン ジャー プロセス RDBSS で現在実装されているは使用しないすべてのシステム リソース清掃の終了が必要になるまでです。 清掃の終了マーク済みである最初のエントリは、スカベンのポストされたタイマー要求になります。 現在の実装でタイマー要求は、1 回限りのタイマー要求として転記されます。 これはエントリの終了される時間間隔に関して一切保証がないことを意味します。 スカベン ジャーのアクティブ化のメカニズムは、後の段階で微調整するための潜在的な候補です。

ルーチンの清掃を消去および RDBSS を以下に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554673" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554673)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、すべてのネットワークのミニ リダイレクターに関連付けられている FOBX 構造を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554679" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554679)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造に関連付けられている FOBX 構造体のすべてを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554707" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554707)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のネットワークのミニ リダイレクター デバイス オブジェクトに関連付けられた FOBX 構造体のすべてを清掃です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554713" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554713)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは清掃 NET_ROOT 構造に関連付けられている FOBX 構造体のすべてです。</p></td>
</tr>
</tbody>
</table>

 

 

 




