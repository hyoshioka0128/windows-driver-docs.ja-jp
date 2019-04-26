---
title: キャビネット ファイル関数
description: キャビネット ファイル関数
ms.assetid: 0f72c833-6bcb-4b11-aa7e-dc5cc678836f
keywords:
- SetupAPI 関数 WDK、キャビネット ファイル
- .cab ファイル
- CAB ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2ad124295c0e42081b0ae38e359e825fa3be5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342778"
---
# <a name="cabinet-file-function"></a>キャビネット ファイル関数





キャビネット (CAB) ファイルは 1 つのファイルでは、通常、します。*cab*ファイル ライブラリとしていくつかの圧縮されたファイルを含む拡張機能。 CAB ファイルは、ユーザーのシステムにコピーされるインストール ファイルの整理に使用されます。 圧縮されたファイルは、いくつかの CAB ファイルに分散できます。

次の関数は、CAB ファイルで使用されます。 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377404" data-raw-source="[&lt;strong&gt;SetupIterateCabinet&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377404)"><strong>SetupIterateCabinet</strong></a></p></td>
<td align="left"><p>CAB ファイルに格納されているファイルごとにコールバック関数への通知を送信します。</p></td>
</tr>
</tbody>
</table>

 

 

 





