---
title: PCL 区切りページのエスケープ コード
description: PCL 区切りページのエスケープ コード
ms.assetid: 8e571fcd-f6ee-4a56-8d8a-20bf3a5c333c
keywords:
- PCL の区切り記号 ページのエスケープ コード WDK PCL XL
- PCL XL ベクター グラフィックス WDK Unidrv、区切りページのエスケープ コード
- エスケープ コード WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef63ceb12b1f08b9367797206a9581d27463917
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464200"
---
# <a name="pcl-separator-page-escape-codes"></a>PCL 区切りページのエスケープ コード





PCL 区切りページを作成するときに、次の表に示すようにエスケープ コードを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エスケープ コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;/p&gt;</td>
<td><p>区切りファイルの最初の行には、この文字のみを含める必要があります。 区切りファイルのインタープリターでは、区切り記号として区切りファイルのコマンドを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p>&lt;em&gt;n</em></p></td>
<td><p>指定された行の数をスキップします<em>n</em> (0 ~ 9) から。 次の行に印刷を移動する 0 行をスキップしています。</p></td>
</tr>
<tr class="odd">
<td><p>\B\M</p></td>
<td><p>\U が出現するまでの文字を二重幅ブロック内のテキストを出力します。</p></td>
</tr>
<tr class="even">
<td><p>\B\S</p></td>
<td><p>\U が出現するまでは、文字の幅が 1 つのブロック内のテキストを出力します。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>ジョブが印刷された日時を出力します。 地域のオプション (Windows 2000) または地域と言語のオプションで指定されている形式で時刻が表示されます (Windows XP 以降) コントロール パネルの します。</p></td>
</tr>
<tr class="even">
<td><p>\E</p></td>
<td><p>プリンターのページを取り出します。 新しい区切りページを開始するか、区切り記号のページング ファイルの末尾には、このコードを使用します。 印刷するときに、余分な空白区切りページを取得する場合は、このコードを区切りページ ファイルから削除します。</p></td>
</tr>
<tr class="odd">
<td><p>\F<em>pathname</em></p></td>
<td><p>指定されたファイルの内容を印刷<em>pathname</em>、空の行に開始します。 このファイルの内容は、処理を行わなくても、プリンターに直接コピーされます。</p></td>
</tr>
<tr class="even">
<td><p>\H<em>nn</em></p></td>
<td><p>プリンター固有のコントロール一連の設定場所<em>nn</em>プリンターに直接送信される 16 進数の ASCII コードに示します。 特定の数値を判断するプリンターのマニュアルを参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>\I</p></td>
<td><p>ジョブの数を出力します。</p></td>
</tr>
<tr class="even">
<td><p>\L<em>xxx</em></p></td>
<td><p>\L エスケープのコードの後に表示されるテキストの文字列を出力します。 \LTest を入力すると、区切りページに"Test"というテキストが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p>\N</p></td>
<td><p>ジョブを送信した人のユーザー名を出力します。</p></td>
</tr>
<tr class="even">
<td><p>\U</p></td>
<td><p>ブロックの文字の印刷をオフにします。</p></td>
</tr>
<tr class="odd">
<td><p>\W<em>nn</em></p></td>
<td><p>区切りページの幅を設定します。 既定の幅は 80 文字、および最大の幅は 256 文字です。 この幅を超える文字が削除されます。</p></td>
</tr>
</tbody>
</table>

 

ローカルの印刷プロバイダー プリント プロセッサおよび区切りページのプロセッサのジョブが成功した後に送信、ジョブ、スプーラーから適切なポートの印刷モニターします。

 

 




