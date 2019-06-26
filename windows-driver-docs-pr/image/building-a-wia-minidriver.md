---
title: WIA ミニドライバーの作成
description: WIA ミニドライバーの作成
ms.assetid: 7a13d355-f42e-406d-8cba-4739df1af9fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f934b2613cf8a15ab1bb8c3f4a55caa42e0a06d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366746"
---
# <a name="building-a-wia-minidriver"></a>WIA ミニドライバーの作成





すべての WIA ミニドライバーでは、次のヘッダー ファイルとライブラリ ファイルが必要です。

### <a name="header-files"></a>ヘッダー ファイル

すべて WIA ミニドライバーは、次の表に表示されるヘッダー ファイルを含める必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ヘッダー ファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>sti.h</em></p></td>
<td><p>STI インターフェイス、構造、およびイベント WIA ミニドライバーが使用できる Guid を定義します。</p></td>
</tr>
<tr class="even">
<td><p><em>stiusd.h</em></p></td>
<td><p>定義、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[IStiUSD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">IStiUSD</a>インターフェイスをすべて WIA ミニドライバーを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>wiamindr.h</em></p></td>
<td><p>定義、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv</a>インターフェイスをすべて WIA ミニドライバーを実装する必要があります。 WIA ミニドライバーによって使用されるその他のインターフェイスはも定義されています。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーは、追加のヘッダー ファイルを必要があります。 必要なヘッダーは、デバイスの種類および実装されている機能に依存します。 これらの要件については、リファレンス セクションで説明します。

### <a name="library-files"></a>ライブラリ ファイル

WIA には、次の表に示すライブラリ ファイルが使用されます。 すべてのミニドライバーは、これらのライブラリが必要です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ライブラリ ファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>wiaguid.lib</em></p></td>
<td><p>エクスポートはクラス id (Clsid) とインターフェイス識別子 (Iid) です。</p></td>
</tr>
<tr class="even">
<td><p><em>wiaservc.lib</em></p></td>
<td><p>WIA サービスのヘルパー関数をエクスポートします。</p></td>
</tr>
</tbody>
</table>

 

WDK ビルド環境で*Include*と*Lib*ディレクトリは検索パス内の最初のディレクトリである必要があります。 これにより、ヘッダーとライブラリ ファイルの最新バージョンを使用していること。

 

 




