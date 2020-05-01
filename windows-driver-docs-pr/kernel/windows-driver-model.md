---
title: Windows Driver Model (WDM)
description: ここのセクションでは、Windows Driver Model (WDM) について、および WDM ドライバー、デバイス構成、ドライバー レイヤー、および WDM のバージョン管理について説明します。
ms.assetid: 9e76c5a8-a19a-44cf-867a-b2246ea8eaf1
keywords:
- カーネル モード ドライバー WDK、WDM ドライバー
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 5d61d773b7e15b1728631a3fabcaaf51ec80d407
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007583"
---
# <a name="windows-driver-model-wdm"></a>Windows Driver Model (WDM)


ここのセクションでは、*Windows Driver Model* (WDM) について、および WDM ドライバー、デバイス構成、ドライバー レイヤー、および WDM のバージョン管理について説明します。 WDM は、複数のバージョンの Windows オペレーティング システムで実行するように記述されたカーネル モード ドライバーの設計を簡略化します。




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
<td><p><em>Windows Driver Model</em> (WDM) は、ドライバー開発者が、すべての Microsoft Windows オペレーティング システムでソースコード互換のデバイス ドライバーを作成できるようにするために導入されました。 WDM ルールに従うカーネル モード ドライバーは <em>WDM ドライバー</em>と呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p><a href="types-of-wdm-drivers.md" data-raw-source="[Types of WDM Drivers](types-of-wdm-drivers.md)">WDM ドライバーの種類</a></p></td>
<td><p>WDM ドライバーには、バス ドライバー、関数ドライバー、およびフィルター ドライバーの 3 種類があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-configurations-and-layered-drivers.md" data-raw-source="[Device Configurations and Layered Drivers](device-configurations-and-layered-drivers.md)">デバイス構成とレイヤー ドライバー</a></p></td>
<td><p>最も一般的なデバイスの種類では、Windows Driver Kit (WDK) によって完全に機能するシステム ドライバーのサンプル セットが提供されます。 個々のサンプル ドライバーは、類似した種類のデバイス用に新しいドライバーを開発するときにモデルとして使用できます。 ただし、システムのドライバーには、新しいデバイス ドライバーを簡単に開発できるようにするという、追加の設計要件がありました。 そのため、類似したデバイスの新しいドライバーをサポートするために特定のドライバーを再利用できるよう、システムのドライバーの多くではレイヤー アーキテクチャが採用されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdm-versions.md" data-raw-source="[WDM Versions](wdm-versions.md)">WDM のバージョン</a></p></td>
<td><p>より新しいバージョンの WDM では、従来のバージョンの WDM で使用できるすべての機能がサポートされています。つまり、新しいバージョンの WDM は、前の WDM バージョンの上位互換になります。 可能であれば、クロス システム ドライバーは、どのオペレーティング システムにおいても最も低いバージョンの WDM に準拠している必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




