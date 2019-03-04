---
title: 公開の制限
description: 次の項目は、公開中に制限されます。 これらの項目の出荷ラベルを作成することもできますが、要求には Microsoft による確認が必要です。
ms.assetid: 30D23457-6BE1-4A4C-B69A-3C8C0A8E093A
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dc3157fb4aed77367bde364bc5a2c15362fd630
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518759"
---
# <a name="publishing-restrictions"></a>公開の制限


次の項目は、公開中に制限されます。 これらの項目の出荷ラベルを作成することもできますが、要求には Microsoft による確認が必要です。

Windows ハードウェア デベロッパー センター ダッシュ ボードでは、これらの公開の制限が適用されます。 公開の制限によって、パートナーは、Microsoft クラス ドライバーや汎用バス HWID 文字列を上書きするドライバーを公開できません。 また、公開の制限によって、汎用のサード パーティ HWID や再利用された HWID による不適切なドライバーを、デバイスが受け取らないようにすることもできます。

これらの制限には、次の表に示す例が含まれますが、これらに限定されるわけではありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>制限の種類</th>
<th>追加情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>無効なドライバーの提出カテゴリの種類</p></td>
<td><p>UNCLASSIFIED</p></td>
</tr>
<tr class="even">
<td><p>無効なアーキテクチャ</p></td>
<td><p>ia64</p></td>
</tr>
<tr class="odd">
<td><p>バス列挙子のない HWID</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>無効なバス列挙子</p></td>
<td><p>ActivCardBus</p>
<p>CIRCLASS</p>
<p>Hid\irdevice</p>
<p>Irbus</p>
<p>PS2_</p>
<p>MIDI</p>
<p>PNP</p>
<p>ACP</p>
<p>IAN</p>
<p>AVM</p>
<p>STREAM</p>
<p>DISPLAY</p></td>
</tr>
<tr class="odd">
<td><p>Classcode の宣言</p></td>
<td><p>\CLASS</p>
<p>\CC</p>
<p>&amp;</p></td>
</tr>
<tr class="even">
<td><p>2 つのパートから成る HWID</p></td>
<td><p>PCI バスや HDAUDIO バスに適用される</p></td>
</tr>
<tr class="odd">
<td><p>サービス UUID があり、ベンダー ID または製品 ID がない Bluetooth HWID</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>無効な PCI ベンダー コード</p></td>
<td><p>0000</p>
<p>FFFF</p></td>
</tr>
<tr class="odd">
<td><p>デバイス コードや製品 ID コードの不備</p></td>
<td><p>PCI バスや USB バスに適用される</p></td>
</tr>
<tr class="even">
<td><p>無効な HWID 文字列の開始</p></td>
<td><p>HID_DEVI</p>
<p>SERIAL_M</p>
<p>ISAPNP\PNP</p>
<p>SERENUM\PNP</p>
<p>PNP</p>
<p><em>PNP</p>
<p>BIOS\PNP</p>
<p>ACPI\PNP</p></td>
</tr>
<tr class="odd">
<td><p>システムで予約済みの HWID</p></td>
<td><p>BIOS\PNP</p>
<p>ACPI\PNP</p></td>
</tr>
<tr class="even">
<td><p>無効な HWID</p></td>
<td><p></em>DONTUSE</p>
<p>SERIAL_MOUSE</p>
<p>Root\circlass</p>
<p>Hid\irdevice</p>
<p>Storage\VolumeSnapshot</p>
<p>Storage\Volume</p></td>
</tr>
</tbody>
</table>

 

ドライバーの公開のワークフローについて詳しくは、[Windows 10 ドライバー公開のワークフローに関するドキュメント](https://go.microsoft.com/fwlink/p/?LinkId=617374)をご覧ください。

 

 





