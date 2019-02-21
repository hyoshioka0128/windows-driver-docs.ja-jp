---
title: IPrintOemCommon COM インターフェイス
description: IPrintOemCommon COM インターフェイス
ms.assetid: 1d4b2f77-6682-4a4b-8d7f-34acd03523e1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b912ca353754dd032cdea40ba349a33d45128dd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551199"
---
# <a name="iprintoemcommon-com-interface"></a>IPrintOemCommon COM インターフェイス


`IPrintOemCommon`プラグインを指定するか、デバイス情報を取得する COM インターフェイスを使用できます。 このインターフェイスは、ユーザー インターフェイスとレンダリング プラグイン間で共通の機能を提供します。

次の表とすべてのメソッドについて説明する`IPrintOemCommon`インターフェイスを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IPrintOemCommon::DevMode</strong></p></td>
<td><p>プライベート DEVMODEW メンバーに対して操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IPrintOemCommon::GetInfo</strong></p></td>
<td><p>プラグインを返します&#39;情報を識別します。</p></td>
</tr>
</tbody>
</table>

 

UI プラグインのこれらのメソッドを実装する方法については、次を参照してください。 [IPrintOemUI COM インターフェイス](iprintoemui-com-interface.md)します。

 

 




