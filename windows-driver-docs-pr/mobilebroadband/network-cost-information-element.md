---
title: ネットワーク コストの情報の要素
description: ネットワーク コストの情報の要素
ms.assetid: 973294b5-0c4f-4056-ad28-62c58f10c232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 347344b72f12e246ce633ec58f8f5cde5612d929
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571378"
---
# <a name="network-cost-information-element"></a>ネットワーク コストの情報の要素


Wi-fi ネットワークのコストをクライアントに通信するためには、Microsoft と 802.11 プロトコルのベンダー拡張機能が定義します。 この拡張機能は、ネットワーク コストの IE です。

**注**   802.11 プロトコルにより、ベンダーが定義した情報要素 (IEs) とそれを無視し、残り IEs の処理を継続する特定の IE を理解していないクライアントが必要です。 これには、他の種類のオペレーティング システムの既存のクライアントと対話する製品に新しい IE を追加する互換性のリスクが最小限に抑えます。

 

次の表では、ネットワーク コストの IE 形式を示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>サイズ (オクテット)</th>
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>属性 ID</p></td>
<td><p>1</p></td>
<td><p>0 xdd を設定</p></td>
<td><p>型 (ベンダー拡張)</p></td>
</tr>
<tr class="even">
<td><p>長さ</p></td>
<td><p>1</p></td>
<td><p>0x08</p></td>
<td><p>次のフィールドの長さ</p></td>
</tr>
<tr class="odd">
<td><p>組織的一意識別子 (OUI)</p></td>
<td><p>3</p></td>
<td><p>0x00、0x50、0xf2 の後ろ</p></td>
<td><p>ベンダー (Microsoft)</p></td>
</tr>
<tr class="even">
<td><p>OUI 型</p></td>
<td><p>1</p></td>
<td><p>パターン</p></td>
<td><p>OUI 型 (ネットワーク コスト)</p></td>
</tr>
<tr class="odd">
<td><p>コストの属性 (必須)</p></td>
<td><p>4</p></td>
<td><p>変数</p></td>
<td><p>DWORD、リトル エンディアン バイト順</p></td>
</tr>
</tbody>
</table>

 

次の図は、属性の cost フィールドの形式を示します。

![コスト属性フィールドの形式](images/fig1-mb-format-cost-attr-field.jpg)

次の表は、可能な限りコスト レベル ビット (1 つが必要です)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>制限しない</p></td>
<td><p>この接続でデータを転送するためない増分のコストが適用されます。</p></td>
</tr>
<tr class="even">
<td><p>0x02</p></td>
<td><p>固定</p></td>
<td><p>データ転送は、従量制課金し、カウント データの制限に対して。 この制限内では、コストの違いは適用されません。</p></td>
</tr>
<tr class="odd">
<td><p>0x04</p></td>
<td><p>変数</p></td>
<td><p>このリンクをすべて使用状況の増分コストが適用されます。</p></td>
</tr>
</tbody>
</table>

 

次の表では、可能な限りコストのフラグのビットを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01 00 00</p></td>
<td><p>データの制限を超える</p></td>
<td><p>データの制限とコストの別のネットワーク使用量を超えましたまたは条件が適用されます。</p></td>
</tr>
<tr class="even">
<td><p>0x02 00 00</p></td>
<td><p>混雑しています。</p></td>
<td><p>ネットワーク オペレーターが発生しているか、可能なアクティビティを削減する負荷が高いと要求を指定してください。</p></td>
</tr>
<tr class="odd">
<td><p>0x04 00 00</p></td>
<td><p>Roaming</p></td>
<td><p>プロバイダーのホーム ネットワークや関連会社の外部接続がローミングしています。</p></td>
</tr>
<tr class="even">
<td><p>0x08 00 00</p></td>
<td><p>データの上限に近づいています</p></td>
<td><p>データの制限の近くの使用率が別のネットワーク コストや条件が早く適用可能性があります。</p></td>
</tr>
</tbody>
</table>

 

次の表は、いくつかサンプル コストの属性値を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>既定の WLAN</p></td>
<td><p>0x00 00 00 01</p></td>
<td><p>無制限の接続。固定のブロード バンド支え WLAN の標準。</p></td>
</tr>
<tr class="even">
<td><p>ポータブル ホット スポットの既定値</p></td>
<td><p>0x00 00 00 02</p></td>
<td><p>従量制課金接続。不明なまたはまだ数に達しました。 制限します。モバイル ブロード バンド接続の Windows の既定値と一致します。</p></td>
</tr>
<tr class="odd">
<td><p>制限/スロットル</p></td>
<td><p>0x00 01 00 01</p></td>
<td><p>ユーザーは、データの制限を超えました。速度が低下しますが、使用制限がさらには適用しません。</p></td>
</tr>
<tr class="even">
<td><p>制限を超える請求/</p></td>
<td><p>0x00 01 00 04</p></td>
<td><p>ユーザーは、データの制限を超えました。追加の使用では、従量課金が発生します。</p></td>
</tr>
<tr class="odd">
<td><p>ポータブル ホット スポット]、[ローミング</p></td>
<td><p>0x00 04 00 04</p></td>
<td><p>接続がローミングされます。ネットワークの状態のため、増分料金が適用されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idaddnetworkcostsupporttoyourdevicespanspan-idaddnetworkcostsupporttoyourdevicespanspan-idaddnetworkcostsupporttoyourdevicespanadd-network-cost-support-to-your-device"></a><span id="Add_network_cost_support_to_your_device"></span><span id="add_network_cost_support_to_your_device"></span><span id="ADD_NETWORK_COST_SUPPORT_TO_YOUR_DEVICE"></span>デバイスにネットワーク コストのサポートを追加します。


1.  デバイスの WLAN ビーコンおよびプローブの応答に固定されているを IE を追加、**ポータブル ホット スポット既定**コスト例の属性値を持つテーブルに表示される値。 このネットワークに自動的に接続する Windows 8、Windows 8.1、または Windows 10 コンピューターを選択することを確認、**ネットワークの使用量を減らす**このネットワークのオプション。

2.  ローミング時の既定値の置換、**ポータブル ホット スポット]、[ローミング**コスト属性の値をサンプルを使用してテーブルに記載されている値。

3.  必要に応じて、他の値を次などの適切なありますケース決定する、パートナー事業者を使用します。

    -   (LTE、HSPA + など)、特定の担ぎの中に無制限

    -   制限を超えた状態を検出するために定義されているチャネル。

    -   データの制限が経過すると演算子で定義された動作です。

4.  必要に応じて、使用する場合、デバイス、Wi-fi による次ホップのネットワークとして、この IE でネットワークを接続し、その値 (またはそのがない場合) を独自の SSID をリレー用に確認します。 存在しない場合は、使用、**既定 WLAN**コスト属性の値をサンプルを使用してテーブルに記載されている値。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[通信チャネル](communication-channels.md)

 

 






