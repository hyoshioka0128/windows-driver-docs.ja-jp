---
title: スマート カード ドライバー ライブラリ
description: スマート カード ドライバー ライブラリ
ms.assetid: 12f67a8d-9281-4f79-88c0-e1c9dff5a05d
keywords:
- スマートカードドライバー WDK、ライブラリ
- ライブラリ WDK スマートカード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d9e98529e8df9e7593a5a4b31a9a1134eb0db3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843571"
---
# <a name="smart-card-driver-library"></a>スマート カード ドライバー ライブラリ


## <span id="_ntovr_smart_card_driver_library"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY"></span>


Microsoft では、スマートカードリーダードライバーが実行する必要のあるほとんどの機能を標準化する一連のルーチンを含むドライバーライブラリを提供しています。 ベンダーから提供されたリーダードライバーは、次の操作を実行するためにこれらのルーチンを呼び出す必要があります。

-   スマートカードリソースマネージャーが必要とするデバイス名を作成するには

-   パラメーターを確認し、IOCTL 呼び出しのエラーを検出するには

-   ATR 文字列を解析してパラメーターを変換するには

-   T = 0 および T = 1 ISO プロトコルをサポートするには

-   逆規約をサポートするには

-   イベントをログに記録するには

-   ドライバーへのアクセスを同期するには

「 [WDM スマートカードドライバールーチン](https://docs.microsoft.com/previous-versions/ff549046(v=vs.85))」セクションでは、ドライバーライブラリルーチンの一覧を示し、各アクションを実行するルーチンを示します。

ドライバーライブラリは、リソースマネージャーがリーダードライバーに送信する IOCTL 要求のほとんどを処理します。 [スマートカードドライバーの ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)セクションには、ドライバーライブラリがリーダードライバーの代わりに処理する ioctl の一覧が表示されます。

スマートカードドライバーライブラリおよびスマートカードドライバーライブラリルーチンを呼び出すドライバーによって、次のファイルが使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイル</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Smclib</em></p></td>
<td align="left"><p>スマートカードライブラリルーチンを呼び出すすべてのドライバーに必要な宣言と定義が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smcnt. h</em></p></td>
<td align="left"><p>スマートカードライブラリルーチンを呼び出す WDM ドライバーに必要な宣言と定義が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Winsmcrd. h</em></p></td>
<td align="left"><p>すべてのスマートカードリーダードライバーとスマートカード対応アプリケーションのグローバルヘッダーファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smclib</em></p></td>
<td align="left"><p>WDM ドライバー用のライブラリのバイナリファイルです。</p></td>
</tr>
</tbody>
</table>

 

 

 





