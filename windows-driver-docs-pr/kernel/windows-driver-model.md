---
title: Windows Driver Model (WDM)
description: ここでは、Windows Driver Model (WDM) について説明し、WDM ドライバー、デバイス構成、ドライバーレイヤー、および WDM のバージョン管理について説明します。
ms.assetid: 9e76c5a8-a19a-44cf-867a-b2246ea8eaf1
keywords:
- カーネルモードドライバー WDK、WDM ドライバー
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 5d61d773b7e15b1728631a3fabcaaf51ec80d407
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007583"
---
# <a name="windows-driver-model-wdm"></a>Windows Driver Model (WDM)


ここでは、 *Windows Driver Model* (wdm) について説明し、wdm ドライバー、デバイス構成、ドライバーレイヤー、および wdm のバージョン管理について説明します。 WDM は、複数のバージョンの Windows オペレーティングシステムで実行するように記述されたカーネルモードドライバーの設計を簡略化します。




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
<td><p>ドライバー開発者が、すべての Microsoft Windows オペレーティングシステムでソースコードと互換性のあるデバイスドライバーを作成できるようにするために、 <em>Windows Driver Model</em> (WDM) が導入されました。 WDM ルールに従うカーネルモードドライバーは、 <em>wdm ドライバー</em>と呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p><a href="types-of-wdm-drivers.md" data-raw-source="[Types of WDM Drivers](types-of-wdm-drivers.md)">WDM ドライバーの種類</a></p></td>
<td><p>WDM ドライバーには、バスドライバー、関数ドライバー、およびフィルタードライバーの3種類があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-configurations-and-layered-drivers.md" data-raw-source="[Device Configurations and Layered Drivers](device-configurations-and-layered-drivers.md)">デバイス構成とレイヤードドライバー</a></p></td>
<td><p>最も一般的な種類のデバイスでは、Windows ドライバーキット (WDK) は、完全に機能するシステムドライバーのサンプルセットを提供します。 個々のサンプルドライバーは、類似した種類のデバイス用に新しいドライバーを開発するときにモデルとして使用できます。 ただし、システムのドライバーには、新しいデバイスドライバーを簡単に開発できるようにするための追加の設計要件がありました。 そのため、システムのドライバーの多くには、類似したデバイスの新しいドライバーをサポートするために、特定のドライバーを再利用できるように、階層化されたアーキテクチャがあります。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdm-versions.md" data-raw-source="[WDM Versions](wdm-versions.md)">WDM のバージョン</a></p></td>
<td><p>新しいバージョンの WDM では、従来のバージョンの WDM で使用できるすべての機能がサポートされています。つまり、新しいバージョンの WDM は、前の WDM バージョンのスーパーセットになります。 可能であれば、クロスシステムドライバーは、どのオペレーティングシステムでも最も低い WDM バージョンに準拠している必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




