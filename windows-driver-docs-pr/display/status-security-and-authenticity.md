---
title: 状態のセキュリティと信頼性
description: 状態のセキュリティと信頼性
ms.assetid: 554d74ee-26fb-4e75-b799-c55c6bdd0153
keywords:
- WDK COPP のステータス情報
- ステータス exchange WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f51d9830df9a37c3d8bc14b782344922c23d3c55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558747"
---
# <a name="status-security-and-authenticity"></a>状態のセキュリティと信頼性


## <span id="ddk_status_security_and_authenticity_gg"></span><span id="DDK_STATUS_SECURITY_AND_AUTHENTICITY_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

次の図には、アプリケーション要求の状態、ビデオのミニポート ドライバーとし、セキュリティで保護されたチャネル経由で、アプリケーションにステータス メッセージを送信するビデオのミニポート ドライバーからのメッセージが表示されます。

![exchange の状態を示す図](images/coppstus.png)

これらのステータス メッセージは、エンベロープに含まれます。 エンベロープには、データと MAC セクションが含まれています。 ビデオのミニポート ドライバーでは、データ整合性キーと、OMAC を使用して、状態データの MAC を計算します。 MAC と OMAC の詳細については、次を参照してください。 [COPP で使用される暗号化プリミティブ](cryptographic-primitives-used-by-copp.md)します。

次の表では、上記の図の値について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>r<sub>アプリ</sub></p></td>
<td align="left"><p>128 ビットのランダムな番号が、アプリケーションによって生成されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>状態</p></td>
<td align="left"><p>可変長の状態データ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MAC<sub>KDI</sub>(r<sub>アプリ</sub>状態)</p></td>
<td align="left"><p>データ整合性のセッション キーを使用して、状態データの 128 ビット MAC。</p></td>
</tr>
</tbody>
</table>

 

 

 





