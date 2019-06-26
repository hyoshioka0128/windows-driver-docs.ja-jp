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
ms.openlocfilehash: 6debdcddf4b10a61c76d80d2f322ab0a1b15d37b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385289"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupiteratecabineta" data-raw-source="[&lt;strong&gt;SetupIterateCabinet&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupiteratecabineta)"><strong>SetupIterateCabinet</strong></a></p></td>
<td align="left"><p>CAB ファイルに格納されているファイルごとにコールバック関数への通知を送信します。</p></td>
</tr>
</tbody>
</table>

 

 

 





