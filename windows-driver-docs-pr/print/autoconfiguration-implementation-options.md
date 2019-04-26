---
title: 自動構成の実装オプション
description: 自動構成の実装オプション
ms.assetid: 78a4e11c-ee6e-4306-b787-2ff7889ff877
keywords:
- 自動構成の WDK プリンター、実装のオプション
- プリンターの自動構成の WDK プリンター、実装のオプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56e7d4fcb56bc79d60d7412cadbe2079b06352aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350742"
---
# <a name="autoconfiguration-implementation-options"></a>自動構成の実装オプション


プリンターのベンダーは、自動構成のサポートを提供する必要はありません。 Microsoft では、既存のインボックス ドライバーは変更されませんが、Windows Vista のドライバーを更新して、自動構成をサポートするように Ihv が促進されます。

Ihv 向けドライバーおよび関連するソフトウェアは、特定の要件を満たす必要がありますの自動構成をサポートするために選択したのかどうかこのソフトウェアの出荷インボックス Windows とします。

自動構成をサポートするための要件は、プリンター ドライバーをどのように実装--プリンター ミニドライバーまたは--モノリシック プリンター ドライバーとカスタム ポート モニターが含まれるかどうかによって異なります。

<a href="" id="minidriver-implementation--custom-extensions-to-a-microsoft-printer-class-driver-or-a-microsoft-port-monitor-"></a>ミニドライバーの実装 (Microsoft プリンター クラス ドライバーまたは Microsoft ポート モニターにはカスタム拡張機能)  
参照してください[ ボックスの自動構成のサポート](in-box-support-for-autoconfiguration.md)

<a href="" id="monolithic-implementation--standalone-printer-driver-"></a>モノリシック実装 (スタンドアロンのプリンター ドライバー)  
参照してください[IHV ドライバーの自動構成](autoconfiguration-in-an-ihv-driver.md)

<a href="" id="custom-port-monitor"></a>カスタム ポート モニター  
参照してください[IHV ポート モニターの自動構成](autoconfiguration-in-an-ihv-port-monitor.md)

**注**   Unidrv ベースまたは Pscript5 ベースのプリンター ドライバーに「Microsoft プリンター クラス ドライバー」を参照します。 「Microsoft ポート モニター」は、標準の TCP/IP ポート モニタまたは、Web Services for Devices (WSD) ポート モニターを指します。

 

 

 




