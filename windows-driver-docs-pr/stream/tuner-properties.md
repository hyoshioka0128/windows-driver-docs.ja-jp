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
ms.openlocfilehash: 7ee3e1290f0a7bfd5ea775e47e55fd2d61c46f29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355036"
---
# <a name="tuner-properties"></a>チューナーのプロパティ


[PROPSETID\_チューナー](https://msdn.microsoft.com/library/windows/hardware/ff567800)ラジオとテレビ チューナーに関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_チューナー プロパティ セット。 2 番目のテーブルには、Windows Vista 以降を実行している AVStream ミニドライバーに実装されているプロパティについて説明します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565825" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565825)"><strong>KSPROPERTY_TUNER_CAPS</strong></a></p></td>
<td><p>テレビなど、サポートされているモードをチューニングおよびラジオのチューニングを含む、チューナー ハードウェアの機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565833" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565833)"><strong>KSPROPERTY_TUNER_FREQUENCY</strong></a></p></td>
<td><p>現在のテレビ チャンネルや無線を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565851" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565851)"><strong>KSPROPERTY_TUNER_INPUT</strong></a></p></td>
<td><p>同軸ケーブルや入力アンテナ チューナーなど、チューナー デバイスへの入力を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565862" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565862)"><strong>KSPROPERTY_TUNER_MODE</strong></a></p></td>
<td><p>アナログ テレビ、デジタル テレビ、ラジオ、DSS などのデバイス モードのチューニングを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565865" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565865)"><strong>KSPROPERTY_TUNER_MODE_CAPS</strong></a></p></td>
<td><p>各個々 のチューニング モードの機能を返します。 返されるアナログのテレビ チューナー機能は、返される機能のチューニング オプションよりも異なるがあります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565907" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565907)"><strong>KSPROPERTY_TUNER_STANDARD</strong></a></p></td>
<td><p>アナログ チューナーの標準、NTSC、PAL、SECAM などを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565921" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565921)"><strong>KSPROPERTY_TUNER_STATUS</strong></a></p></td>
<td><p>現在の頻度、PLL オフセット、信号強度など、チューナーのプロセスの現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565842" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565842)"><strong>KSPROPERTY_TUNER_IF_MEDIUM</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565887" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565887)"><strong>KSPROPERTY_TUNER_SCAN_CAPS</strong></a></p></td>
<td><p>サポートされているブロードキャスト ネットワークの種類とチューニングのデバイスがシグナルのスキャンとスキャンの結果に関する通知をサポートするかどうかを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565893" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565893)"><strong>KSPROPERTY_TUNER_SCAN_STATUS</strong></a></p></td>
<td><p>シグナルのスキャンの状態を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565909" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565909)"><strong>KSPROPERTY_TUNER_STANDARD_MODE</strong></a></p></td>
<td><p>チューナーが信号をチューナーの標準を自動的に検出するかどうかを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565881" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565881)"><strong>KSPROPERTY_TUNER_NETWORKTYPE_SCAN_CAPS</strong></a></p></td>
<td><p>チューニングのデバイスをサポートする特定のブロードキャスト ネットワークの種類のスキャン機能を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




