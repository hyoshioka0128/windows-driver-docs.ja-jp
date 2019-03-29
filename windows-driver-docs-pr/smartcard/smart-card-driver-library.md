---
title: スマート カード ドライバー ライブラリ
description: スマート カード ドライバー ライブラリ
ms.assetid: 12f67a8d-9281-4f79-88c0-e1c9dff5a05d
keywords:
- スマート カードのドライバー WDK、ライブラリ
- ライブラリの WDK スマート カード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682f9bbd6f6bcacd2c2722b4315b03a1730fcae9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349159"
---
# <a name="smart-card-driver-library"></a>スマート カード ドライバー ライブラリ


## <span id="_ntovr_smart_card_driver_library"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY"></span>


Microsoft では、ほとんどのスマート カード リーダーのドライバーを実行する必要があります関数を標準化するルーチンのセットを含むドライバー ライブラリを提供します。 ベンダーから提供されたリーダーのドライバーでは、次の操作を実行するこれらのルーチンを呼び出す必要があります。

-   スマート カード リソース マネージャーが必要なデバイス名を作成するには

-   パラメーターを確認し、IOCTL 呼び出しのエラーを検出するには

-   ATR 文字列を解析し、パラメーターを変換するには

-   T = 0 および ISO T = 1 のプロトコルをサポートするには

-   逆の規則をサポートするには

-   イベントを記録するには

-   ドライバーへのアクセスを同期するには

[WDM スマート カードのドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff549046)セクション、ドライバーのライブラリ ルーチンを挙げ、各アクションを実行するルーチンを識別します。

ドライバー ライブラリは、ほとんどのリソース マネージャーは、リーダーのドライバーに送信する IOCTL 要求を処理します。 [スマート カードのドライバーの Ioctl](https://msdn.microsoft.com/library/windows/hardware/ff548988)セクションで、リーダーのドライバーに代わってドライバー ライブラリを処理する Ioctl を一覧表示されます。

次のファイルは、スマート カードのドライバー ライブラリのルーチンを呼び出すドライバーとスマート カードのドライバー ライブラリによって使用されます。

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
<td align="left"><p><em>Smclib.h</em></p></td>
<td align="left"><p>宣言とスマート カードのライブラリ ルーチンを呼び出すすべてのドライバーで必要な定義が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smcnt.h</em></p></td>
<td align="left"><p>宣言とスマート カードのライブラリ ルーチンを呼び出す WDM ドライバーで必要な定義が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Winsmcrd.h</em></p></td>
<td align="left"><p>すべてのスマート カード リーダーのドライバーとスマート カード対応アプリケーションのグローバルのヘッダー ファイルです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smclib.sys</em></p></td>
<td align="left"><p>WDM ドライバー ライブラリのバイナリ ファイル。</p></td>
</tr>
</tbody>
</table>

 

 

 





