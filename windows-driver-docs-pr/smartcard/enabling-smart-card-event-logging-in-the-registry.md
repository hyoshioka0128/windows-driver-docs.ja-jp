---
title: スマート カードのイベント ログ、レジストリの有効化
description: スマート カードのイベント ログ、レジストリの有効化
ms.assetid: b07ff2d7-9025-424e-a57e-eb37ae4091f4
keywords:
- スマート カードのドライバー WDK、レジストリ
- レジストリの WDK スマート カード
- ログの WDK スマート カード
- WDK スマート カードのイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a11ff11966b535c33469849eb052b90e1db9a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538768"
---
# <a name="enabling-smart-card-event-logging-in-the-registry"></a>スマート カードのイベント ログ、レジストリの有効化


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

 

これらのレジストリ エントリを指定する方法については、次を参照してください。 [ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)します。

 

 





