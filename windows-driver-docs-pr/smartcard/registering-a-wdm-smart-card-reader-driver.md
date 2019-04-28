---
title: WDM スマート カード リーダー ドライバーの登録
description: WDM スマート カード リーダー ドライバーの登録
ms.assetid: 0f82c18b-3bbc-4bc6-825a-58e957f4e3aa
keywords:
- スマート カードのドライバー WDK、レジストリ
- レジストリの WDK スマート カード
- WDK のスマート カードを登録する WDM デバイス
- スマート カードのドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21003952ed0e6527b9e25b78b51a6175ba4ce128
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379771"
---
# <a name="registering-a-wdm-smart-card-reader-driver"></a>WDM スマート カード リーダー ドライバーの登録


## <span id="_ntovr_registering_a_wdm_smart_card_reader_driver"></span><span id="_NTOVR_REGISTERING_A_WDM_SMART_CARD_READER_DRIVER"></span>


スマート カード リーダーのドライバーをデバイス マネージャーに表示するには、次のキーの下の該当のレジストリ値を配置する必要があります。

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\**<em>SmartCardDriver</em>

必要な値は、次の表に表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ値の名前</th>
<th align="left">レジストリ値の内容</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>スタート</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000002</strong></p></td>
<td align="left"><p>値が 2 は、自動的に開始ドライバーです。 開発中は、使用、<strong>開始</strong>ドライバーを手動で開始する 3 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>型</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000001</strong></p></td>
<td align="left"><p>値 1 では、カーネル モード ドライバーとしてドライバーを識別します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>グループ化</strong></p></td>
<td align="left"><p><strong>SmartCardReader</strong></p></td>
<td align="left"><p>すべてのドライバーがのメンバーであるが、 <strong>SmartCardReader</strong>クラスのセットアップを開始するには、このクラスのスマート カード リソース マネージャーが待機するためです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ErrorControl</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000001</strong></p></td>
<td align="left"><p>1 の値を読み込むには、ドライバーが失敗した場合、エラー メッセージには、起動して、システムことができます。</p></td>
</tr>
</tbody>
</table>

 

 

 





