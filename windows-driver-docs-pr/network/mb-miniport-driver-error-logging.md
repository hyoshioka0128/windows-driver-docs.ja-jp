---
title: MB ミニポート ドライバー エラー ログ
description: MB ミニポート ドライバー エラー ログ
ms.assetid: 57f83d03-29e5-4a20-8c0c-2d00954e7ccb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 015bf2fe6831729d7a624c2bc938751cb89f48f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343320"
---
# <a name="mb-miniport-driver-error-logging"></a>MB ミニポート ドライバー エラー ログ


MB のミニポート ドライバーでは、次のチェックを実行する必要があります、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)などの関数。

-   MB ドライバー モデルをサポートするために必要な正しいデバイス ファームウェア バージョンが存在します。

-   デバイスとの通信に使用可能な COM ポート。

-   リソース競合はありません。

NDIS を返す必要がありますミニポート ドライバーに必要なリソースの取得に失敗すると、\_状態\_その MiniportInitializeEx 関数からのリソース。 ミニポート ドライバーを呼び出す必要があります[ **NdisWriteErrorLogEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff564663)エラーの詳細を Windows イベント ログに記録します。

ミニポート ドライバーは、次の表の情報に従って NdisWriteErrorLogEntry (可変サイズの配列を ULONGs) への呼び出しの最後のパラメーターの最初の要素でエラー コードを指定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_UNSUPPORTED_FIRMWARE</p></td>
<td align="left"><p>デバイスがサポートされていないファームウェア バージョンを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_ERROR_COM_PORT_CONFLICT</p></td>
<td align="left"><p>デバイスと通信するための COM ポートを開くことができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_ERROR_RESOURCE_CONFLICT_OTHER</p></td>
<td align="left"><p>リソース競合します。</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーでは、可変サイズの配列の要素の残りの部分を他の値を格納できます。

 

 





