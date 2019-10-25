---
title: WIA ミニドライバーの作成
description: WIA ミニドライバーの作成
ms.assetid: 7a13d355-f42e-406d-8cba-4739df1af9fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8493f6d3f64d2513f8ad5614171247fb4599f1d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840886"
---
# <a name="building-a-wia-minidriver"></a>WIA ミニドライバーの作成





すべての WIA ミニドライバーでは、次のヘッダーファイルとライブラリファイルが必要です。

### <a name="header-files"></a>ヘッダーファイル

すべての WIA ミニドライバーには、次の表に示すヘッダーファイルが含まれている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ヘッダーファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>sti</em></p></td>
<td><p>WIA ミニドライバーが使用できる、STI インターフェイス、構造体、およびイベント Guid を定義します。</p></td>
</tr>
<tr class="even">
<td><p><em>同米ドル</em></p></td>
<td><p>すべての WIA ミニドライバーが実装する必要がある<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IStiUSD](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">Iと米国</a>のインターフェイスを定義します。</p></td>
</tr>
<tr class="odd">
<td><p><em>wiamindr. h</em></p></td>
<td><p>すべての WIA ミニドライバーが実装する必要のある<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv</a>インターフェイスを定義します。 ここでは、WIA ミニドライバーによって使用されるその他のインターフェイスも定義されています。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーでは、追加のヘッダーファイルが必要になる場合があります。 必要なヘッダーは、デバイスの種類と実装されている機能によって異なります。 これらの要件については、「参照」セクションで説明します。

### <a name="library-files"></a>ライブラリファイル

WIA では、次の表に示すライブラリファイルが使用されます。 すべてのミニドライバーにこれらのライブラリが必要です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ライブラリファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>wiaguid .lib</em></p></td>
<td><p>クラス識別子 (Clsid) とインターフェイス識別子 (Iid が) をエクスポートします。</p></td>
</tr>
<tr class="even">
<td><p><em>wiaservc</em></p></td>
<td><p>WIA サービスヘルパー関数をエクスポートします。</p></td>
</tr>
</tbody>
</table>

 

ビルド環境では、WDK *Include*ディレクトリと*Lib*ディレクトリが検索パスの最初のディレクトリになる必要があります。 これにより、ヘッダーファイルとライブラリファイルの最新バージョンが確実に使用されます。

 

 




