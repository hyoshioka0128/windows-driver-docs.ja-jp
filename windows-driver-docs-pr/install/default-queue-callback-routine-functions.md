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
ms.openlocfilehash: 02d05d5de76c19fbbd777d6c587b7b0c763c25f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360850"
---
# <a name="default-queue-callback-routine-functions"></a>既定のキュー コールバック ルーチン関数





ファイルのキューからコールバック ルーチンを関連付ける場合、コールバック ルーチンには、システムがキューに置かれたファイルの操作のいずれかを実行するたびが呼び出されます。 通常、既定のキュー コールバック ルーチンを使用できます[ **SetupDefaultQueueCallback**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka)、これらの通知を処理します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka" data-raw-source="[&lt;strong&gt;SetupDefaultQueueCallback&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka)"><strong>SetupDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>キューに置かれたときに、システムによって送信された通知を処理するファイル操作が実行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupinitdefaultqueuecallback" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallback&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupinitdefaultqueuecallback)"><strong>SetupInitDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>必要とされるコンテキスト情報を初期化します<strong>SetupDefaultQueueCallback</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupinitdefaultqueuecallbackex" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallbackEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupinitdefaultqueuecallbackex)"><strong>SetupInitDefaultQueueCallbackEx</strong></a></p></td>
<td align="left"><p>必要とされるコンテキスト情報を初期化します<strong>SetupDefaultQueueCallback</strong>、および進行状況メッセージを表示するための別のウィンドウを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuptermdefaultqueuecallback" data-raw-source="[&lt;strong&gt;SetupTermDefaultQueueCallback&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuptermdefaultqueuecallback)"><strong>SetupTermDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>システム通知を<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-installation-application" data-raw-source="&lt;em&gt;device installation application&lt;/em&gt;"><em>デバイス インストール アプリケーション</em></a>追加のファイルのキュー操作はコミットされません。</p></td>
</tr>
</tbody>
</table>

 

 

 





