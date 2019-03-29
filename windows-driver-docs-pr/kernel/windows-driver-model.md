---
title: Windows Driver Model (WDM)
description: このセクションでは、Windows Driver Model (WDM) について説明し、WDM ドライバー、デバイスの構成、ドライバーの階層化、および WDM バージョン管理の種類について説明します。
ms.assetid: 9e76c5a8-a19a-44cf-867a-b2246ea8eaf1
keywords:
- カーネル モード ドライバー WDK、WDM ドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8374c462e319a70ca92430cec01a41b310020238
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350003"
---
# <a name="windows-driver-model-wdm"></a>Windows Driver Model (WDM)


このセクションについて説明します、 *Windows Driver Model* (WDM)、および WDM ドライバー、デバイスの構成、ドライバーの階層化、および WDM バージョン管理の種類について説明します。 WDM は、複数のバージョンの Windows オペレーティング システムで実行に書き込まれるカーネル モード ドライバーの設計を簡略化します。




## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="introduction-to-wdm.md" data-raw-source="[Introduction to WDM](introduction-to-wdm.md)">WDM の概要</a></p></td>
<td><p>開発者がソース コードと互換性のあるすべての Microsoft Windows で動作しているシステムでは、デバイス ドライバーを記述する、 <em>Windows Driver Model</em> (WDM) が導入されました。 WDM 規則に従うカーネル モード ドライバーが呼び出されて<em>WDM ドライバー</em>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="types-of-wdm-drivers.md" data-raw-source="[Types of WDM Drivers](types-of-wdm-drivers.md)">WDM ドライバーの種類</a></p></td>
<td><p>WDM ドライバーの 3 つの種類があります。 バス ドライバー、ドライバーの関数、およびフィルター ドライバー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-configurations-and-layered-drivers.md" data-raw-source="[Device Configurations and Layered Drivers](device-configurations-and-layered-drivers.md)">デバイスの構成と複数層のドライバー</a></p></td>
<td><p>最も一般的な種類のデバイスでは、Windows Driver Kit (WDK) は完全に機能するシステムのドライバーのサンプル セットを提供します。 ような種類のデバイス用の新しいドライバーを開発するときに、個々 のサンプルのドライバーをモデルとして使用できます。 ただし、システムのドライバーが、追加のデザイン要件必要がある。 新しいデバイス ドライバーを開発しやすくします。 その結果、多くのシステムのドライバーがある階層型アーキテクチャ類似するデバイスの新しいドライバーをサポートするために特定のドライバーを再利用できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdm-versions.md" data-raw-source="[WDM Versions](wdm-versions.md)">WDM バージョン</a></p></td>
<td><p>WDM の以降のバージョンは一般に WDM; の以前のバージョンで使用可能なすべての機能をサポートします。これは WDM の新しい各バージョンでは、WDM の以前のバージョンのスーパー セットがあります。 可能であれば、システム間 driver が任意のオペレーティング システムで最も低い WDM バージョンに従う必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




