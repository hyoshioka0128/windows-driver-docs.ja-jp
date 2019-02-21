---
title: 既定のキュー コールバック ルーチン関数
description: 既定のキュー コールバック ルーチン関数
ms.assetid: 46d767ed-cfeb-4bd0-8792-08781a1335d6
keywords:
- 関数は、SetupAPI の WDK、既定のキューのコールバック ルーチン
- 既定のキューのコールバック ルーチン
- キュー コールバック ルーチン WDK SetupAPI
- コールバック ルーチン WDK SetupAPI
- キューに WDK SetupAPI ファイル
- キューの WDK SetupAPI ファイルします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da8b6c4d54e6bb8055efc3bdeecd84c5a5909a64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532697"
---
# <a name="default-queue-callback-routine-functions"></a>既定のキュー コールバック ルーチン関数





ファイルのキューからコールバック ルーチンを関連付ける場合、コールバック ルーチンには、システムがキューに置かれたファイルの操作のいずれかを実行するたびが呼び出されます。 通常、既定のキュー コールバック ルーチンを使用できます[ **SetupDefaultQueueCallback**](https://msdn.microsoft.com/library/windows/desktop/aa376993)、これらの通知を処理します。

次の表は、キューの既定のコールバック ルーチンに関連付けられている関数を一覧表示します。 関数の詳細な説明については、およびファイルのキューでコールバック ルーチンを使用する方法の詳細については、Microsoft Windows SDK のマニュアルを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376993" data-raw-source="[&lt;strong&gt;SetupDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376993)"><strong>SetupDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>キューに置かれたときに、システムによって送信された通知を処理するファイル操作が実行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377395" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377395)"><strong>SetupInitDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>必要とされるコンテキスト情報を初期化します<strong>SetupDefaultQueueCallback</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377396" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallbackEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377396)"><strong>SetupInitDefaultQueueCallbackEx</strong></a></p></td>
<td align="left"><p>必要とされるコンテキスト情報を初期化します<strong>SetupDefaultQueueCallback</strong>、および進行状況メッセージを表示するための別のウィンドウを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377442" data-raw-source="[&lt;strong&gt;SetupTermDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377442)"><strong>SetupTermDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>システム通知を<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-installation-application" data-raw-source="&lt;em&gt;device installation application&lt;/em&gt;"><em>デバイス インストール アプリケーション</em></a>追加のファイルのキュー操作はコミットされません。</p></td>
</tr>
</tbody>
</table>

 

 

 





