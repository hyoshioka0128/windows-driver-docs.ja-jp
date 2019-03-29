---
title: LogViewer 表示の読み取り
description: LogViewer 表示の読み取り
ms.assetid: 425aff5d-780e-4600-a43a-8012d70263f1
keywords:
- LogViewer、表示
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7edf95aba0116d9326e96e57c388f2f26108ec5e
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463813"
---
# <a name="reading-the-logviewer-display"></a>LogViewer 表示の読み取り


## <span id="ddk_reading_the_logviewer_display_dtoolq"></span><span id="DDK_READING_THE_LOGVIEWER_DISPLAY_DTOOLQ"></span>


LogViewer では、ログに記録された順序ですべての関数の一覧が表示されます。

ディスプレイの各行には、複数の列が含まれています。 各列の意味は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[列]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>この列が含まれている場合、この関数は、1 つまたは複数のパラメーターを受け取ります「+」(プラス記号)、ことを示します。 パラメーターとその値を表示するには、行をダブルクリックするか、行が赤に記載されているときに、右矢印キーを押します。 再び非表示に、もう一度クリックを 2 倍または行が赤に記載されているときに、左矢印キーを押します。</p>
<p>このコラムでは、「d 番号」値があります。 これには、関数呼び出しの「奥行き」(つまり、深さの呼び出しが他のログに記録された関数の呼び出しで入れ子になっている) ことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>関数呼び出しの連続する行の数。 これは、フィルターを適用し、どの程度離れた 2 つの関数呼び出しに関心がある場合に便利ですが。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Thrd</strong></p></td>
<td align="left"><p>関数呼び出しを行ったスレッドの数。 この数は、スレッド ID ではありませんではなく、割り当てられた番号に基づいてスレッドは、プロセスで作成された順序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>呼び出し元</strong></p></td>
<td align="left"><p>命令ポインター アドレス、関数の呼び出しが行われます。 これは、呼び出しの戻り値のアドレスから派生します。 -5 バイトのリターン アドレス実際には (の一般的なサイズを<strong>dword ptr を呼び出す</strong>命令)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Module</strong></p></td>
<td align="left"><p>このモジュールは、呼び出し元の命令が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>API 関数</strong></p></td>
<td align="left"><p>関数の名前。 簡潔にするための関数を含むモジュールの名前は省略されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>戻り値</strong></p></td>
<td align="left"><p>Void 関数ではない場合、関数によって返される値。</p></td>
</tr>
</tbody>
</table>

 

ビューアーに行をダブルクリックして、関数および関数に「移動」の値にパラメーターを表示する行を展開します。 OUT パラメーターとして指定する必要が場合、は、「出力されている」の値が右側に表示されます。

展開し、行を折りたたむ、ENTER キーまたは右と左方向キーを使用することもできます。

状態コード エラーを返す関数呼び出しはピンク色で網掛け表示されます。

 

 





