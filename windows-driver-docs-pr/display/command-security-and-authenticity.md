---
title: コマンドのセキュリティと信頼性
description: コマンドのセキュリティと信頼性
ms.assetid: 2a70f974-c34c-4462-a772-d8253f842ed8
keywords:
- WDK COPP コマンド
- exchange WDK COPP コマンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e27ce3bab19312abf3f704d377e7873521441cb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582359"
---
# <a name="command-security-and-authenticity"></a>コマンドのセキュリティと信頼性


## <span id="ddk_command_security_and_authenticity_gg"></span><span id="DDK_COMMAND_SECURITY_AND_AUTHENTICITY_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次の図は、セキュリティで保護されたチャネル経由でビデオのミニポート ドライバーにコマンド メッセージを送信するアプリケーションを示します。

![exchange のコマンドを示す図](images/coppcmnd.png)

これらのコマンドのメッセージは、エンベロープに含まれます。 エンベロープには、データと MAC セクションが含まれています。 アプリケーションでは、データ整合性キーと、OMAC を使用して、MAC のコマンドのデータを計算します。 MAC と OMAC の詳細については、[COPP で使用される暗号化プリミティブ](cryptographic-primitives-used-by-copp.md)を参照してください。

次の表では、上記の図の値について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>コマンド</p></td>
<td align="left"><p>コマンドの可変長のデータ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC<sub>KDI</sub>(コマンド)</p></td>
<td align="left"><p>データ整合性のセッション キーを使用してデータをコマンドの 128 ビット MAC。</p></td>
</tr>
</tbody>
</table>

 

 

 





