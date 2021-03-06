---
title: スマート カードのイベント ログをレジストリで有効にする
description: スマート カードのイベント ログをレジストリで有効にする
ms.assetid: b07ff2d7-9025-424e-a57e-eb37ae4091f4
keywords:
- スマート カードのドライバー WDK、レジストリ
- レジストリの WDK スマート カード
- ログの WDK スマート カード
- WDK スマート カードのイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d3916d0dfe7527f174ac37b5a54ca1242c6c23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356719"
---
# <a name="enabling-smart-card-event-logging-in-the-registry"></a>スマート カードのイベント ログをレジストリで有効にする


## <span id="_ntovr_enabling_smart_card_event_logging_in_the_registry"></span><span id="_NTOVR_ENABLING_SMART_CARD_EVENT_LOGGING_IN_THE_REGISTRY"></span>


スマート カード リーダーのドライバーは、システム管理者は、ドライバーが失敗した理由を診断に役立つログを使用できるように、システム イベント ログにエラーを記録する必要があります。

イベント ログを有効にするには、次のキーの下のレジストリにいくつかの値を追加する必要があります。

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\EventLog\\System\\** *SmartCardDriver*

イベントのログ記録を有効にするレジストリ値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ値の名前</th>
<th align="left">レジストリ値の内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>EventMessageFile</strong></p></td>
<td align="left"><p><em>%SystemRoot%\System32\Drivers\SmartCardDriver.sys</em></p>
<div class="alert">
<strong>重要な</strong>  では、ファイル名拡張子を含める必要がある、 <strong>EventMessageFile</strong>値の名前が必要があります、レジストリ パスの他の部分に表示されません。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>TypesSupported</strong></p></td>
<td align="left"><p><strong>DWORD:0x00000007</strong></p></td>
</tr>
</tbody>
</table>

 

これらのレジストリ エントリを指定する方法については、次を参照してください。 [ **INF AddService ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)します。

 

 





