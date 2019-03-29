---
title: 認証済みのキー交換
description: 認証済みのキー交換
ms.assetid: cd8c29ab-6276-4236-9b9c-152adf2868c3
keywords:
- 認証されたキー交換 WDK COPP
- キー交換 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244120aed1b91c30fa13a61aed64e4f218ac526a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570460"
---
# <a name="authenticated-key-exchange"></a>認証済みのキー交換


## <span id="ddk_authenticated_key_exchange_gg"></span><span id="DDK_AUTHENTICATED_KEY_EXCHANGE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次の図は、認証、キーの交換を介してセキュリティで保護された接続の確立を示します。 最初に、ビデオのミニポート ドライバーでは、アプリケーションにグラフィックス ハードウェアの証明書が用意されています。 次に、アプリケーションでは、グラフィックス ハードウェアの証明書から公開キーを抽出します。 アプリケーションは、データ整合性キーを生成した後 (k<sub>DI</sub>)、アプリケーションでは、公開キーを使用して、データ整合性キーが含まれていて、ドライバーにシーケンスを提供するシーケンスを暗号化します。

コマンド、およびステータス メッセージが暗号化されていない; に渡される、その後ただし、各メッセージに対して、mac コンピューターは、データ整合性キーを使用して作成されます。

![図に示す認証とキーの交換](images/coppkey.png)

Mac コンピューターの詳細については、次を参照してください。 [COPP で使用される暗号化プリミティブ](cryptographic-primitives-used-by-copp.md)します。

次の表では、上記の図の値について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>r<sub>GH</sub></p></td>
<td align="left"><p>128 ビット、ドライバーによって生成されたランダムな番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>証明書<sub>GH</sub></p></td>
<td align="left"><p>可変長のデジタル証明がグラフィックス ハードウェアで使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P<sub>GH</sub>(r<sub>GH</sub>、k<sub>DI</sub>status_start、command_start)</p></td>
<td align="left"><p>連結して 1 つ、次のもので構成される、セキュリティで保護されたチャネルのシーケンスを開始します。</p>
<ul>
<li><p>128 ビット、ドライバーによって生成されたランダムな番号。</p></li>
<li><p>アプリケーションによって生成される 128 ビットのランダムなデータ整合性のセッション キー。</p></li>
<li><p>32 ビット ランダムな開始状態シーケンス番号、アプリケーションによって生成されます。</p></li>
<li><p>32 ビット ランダムな開始コマンド シーケンス番号、アプリケーションによって生成されます。</p></li>
</ul>
<p>アプリケーションでは、グラフィック ハードウェアの証明書から取得した公開キーを使用して、シーケンスを暗号化します。 シーケンスは、2,048 ビット長。シーケンスの残りの部分は、0 で埋められます。</p></td>
</tr>
</tbody>
</table>

 

 

 





