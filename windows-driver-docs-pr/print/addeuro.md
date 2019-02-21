---
title: AddEuro
description: AddEuro
ms.assetid: 1d27fbb0-787f-4fb2-8a1c-3c68598d6d41
keywords:
- ミニドライバー WDK Pscript、AddEuro 機能
- AddEuro 機能 WDK の印刷
- ユーロ通貨記号 WDK の印刷
- 欧州連合シンボル WDK の印刷
- ADHasEuro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b6f9b92332844915598b403820d54363f3832e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551461"
---
# <a name="addeuro"></a>AddEuro





ユーロ記号が次の図に示すようには、欧州連合の国/地域で使用される基本的な通貨単位の通貨記号。

![ユーロ通貨記号の図](images/euro.png)

AddEuro 機能は、プリンターのデバイスのフォントに、このシンボルを追加します。 AddEuro を有効にすると、ディスプレイ デバイスに表示されるユーロの通貨記号は印刷することも紙にドキュメントがプリンターに送信されるときにします。 この機能が利用できない、または無効になっている場合、エイリアスを使用しないデバイスのフォントを選択したユーザーは画面で、ユーロ通貨記号を表示されますが、紙に大きな循環ドットが表示されます。 この機能を有効にすると、ユーザーはデバイス フォントをプリンターの利用可能なかどうか、ユーロ記号を印刷できます。

AddEuro はプライベート*PPD*キーワード、 \* **ADHasEuro**プリンタの製造元、最適な既定値を設定することを許可する。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>キーワードと値</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>ADHasEuro</strong>:True</p></td>
<td><p>プリンターが既にダウンロードする必要のない組み込みユーロ通貨記号を使用しています。 この値は、AddEuro は既定で無効になります。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADHasEuro</strong>:False</p></td>
<td><p>プリンターには、組み込みのユーロ記号はありません。用のアプリケーションによって呼び出されると、このシンボルをダウンロードする必要があります。 この値は、AddEuro は、PostScript バージョンに関係なく、既定で有効です。</p></td>
</tr>
</tbody>
</table>

 

場合、 \* **ADHasEuro**キーワードが表示されない、AddEuro 機能が 3011、前に PostScript バージョンとプリンターの既定で有効になっているし、バージョン 3011 以降は既定で無効になっています。

 

 




