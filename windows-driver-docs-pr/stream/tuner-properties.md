---
title: チューナーのプロパティ
description: チューナーのプロパティ
ms.assetid: 43a0c018-fb0e-4a45-9c9a-5896f1e728ac
keywords:
- チューナー プロパティ WDK ビデオのキャプチャします。
- PROPSETID_TUNER
- ラジオ チューナー プロパティ WDK ビデオのキャプチャします。
- テレビ チューナー プロパティ WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6559af5ab5433c82e7bff6e2260689049982b36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377713"
---
# <a name="tuner-properties"></a>チューナーのプロパティ


[PROPSETID\_チューナー](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-tuner)ラジオとテレビ チューナーに関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_チューナー プロパティ セット。 2 番目のテーブルには、Windows Vista 以降を実行している AVStream ミニドライバーに実装されているプロパティについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TUNER KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps)"><strong>KSPROPERTY_TUNER_CAPS</strong></a></p></td>
<td><p>テレビなど、サポートされているモードをチューニングおよびラジオのチューニングを含む、チューナー ハードウェアの機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency)"><strong>KSPROPERTY_TUNER_FREQUENCY</strong></a></p></td>
<td><p>現在のテレビ チャンネルや無線を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-input" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-input)"><strong>KSPROPERTY_TUNER_INPUT</strong></a></p></td>
<td><p>同軸ケーブルや入力アンテナ チューナーなど、チューナー デバイスへの入力を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-mode)"><strong>KSPROPERTY_TUNER_MODE</strong></a></p></td>
<td><p>アナログ テレビ、デジタル テレビ、ラジオ、DSS などのデバイス モードのチューニングを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-mode-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-mode-caps)"><strong>KSPROPERTY_TUNER_MODE_CAPS</strong></a></p></td>
<td><p>各個々 のチューニング モードの機能を返します。 返されるアナログのテレビ チューナー機能は、返される機能のチューニング オプションよりも異なるがあります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-standard" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-standard)"><strong>KSPROPERTY_TUNER_STANDARD</strong></a></p></td>
<td><p>アナログ チューナーの標準、NTSC、PAL、SECAM などを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)"><strong>KSPROPERTY_TUNER_STATUS</strong></a></p></td>
<td><p>現在の頻度、PLL オフセット、信号強度など、チューナーのプロセスの現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-if-medium" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-if-medium)"><strong>KSPROPERTY_TUNER_IF_MEDIUM</strong></a></p></td>
<td><p>デジタル テレビをサポートするチューナー デバイスの中間頻度暗証番号 (pin) の暗証番号 (pin) のメディアを返します。</p></td>
</tr>
</tbody>
</table>

 

次の表は、PROPSETID\_Windows Vista の新しいチューナー プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TUNER KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps)"><strong>KSPROPERTY_TUNER_SCAN_CAPS</strong></a></p></td>
<td><p>サポートされているブロードキャスト ネットワークの種類とチューニングのデバイスがシグナルのスキャンとスキャンの結果に関する通知をサポートするかどうかを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)"><strong>KSPROPERTY_TUNER_SCAN_STATUS</strong></a></p></td>
<td><p>シグナルのスキャンの状態を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-standard-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-standard-mode)"><strong>KSPROPERTY_TUNER_STANDARD_MODE</strong></a></p></td>
<td><p>チューナーが信号をチューナーの標準を自動的に検出するかどうかを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps)"><strong>KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS</strong></a></p></td>
<td><p>チューニングのデバイスをサポートする特定のブロードキャスト ネットワークの種類のスキャン機能を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




