---
title: NDIS 6.20 が動作する中間のドライバーのポートへの変更の概要
description: NDIS 6.20 が動作する中間のドライバーを移植するために必要な変更の概要
ms.assetid: 1ed2b2f6-f337-4aaa-9ce8-90adf7d05722
keywords:
- NDIS 6.20 WDK、中間のドライバーの移植
- NDIS 6.20 WDK に中間のドライバーの移植
- 中間ドライバー WDK
- 中間ドライバー WDK、NDIS 6.20 が動作への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db041a9df84df68357d18217f1434f69465e2ce9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549831"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-620"></a>NDIS 6.20 が動作する中間のドライバーを移植するために必要な変更の概要





このトピックでは、NDIS 6 を移植するために必要な変更をまとめたものです。*x* NDIS 6.20 が動作する中間ドライバー。

NDIS 6.20 が動作環境をサポートするために中間のドライバーを更新するには、NDIS 6 を変更する必要があります。*x*中間ドライバを次のようにします。

<a href="" id="build-environment-------"></a>**環境を構築します。**   
-   NDIS60 プリプロセッサの定義を置き換えます\_ミニポート\_ドライバーまたは NDIS61\_ミニポート\_NDIS620 ドライバー\_ミニポート\_ドライバー。

-   NDIS620 NDIS61 または NDIS60 プリプロセッサの定義に置き換えます。

<a href="" id="general-porting-requirements-------"></a>**移植の一般的な要件**   
-   プロトコル ドライバーおよびミニポート ドライバーの変更はない限りそれ以外の場合も中間ドライバーに適用されます。 これらのドライバーの移植の詳細については、プロトコル ドライバーに移植の概要を参照してください[概要の変更に必要なポートの NDIS 6.20 が動作するためのプロトコル ドライバー](summary-of-changes-required-to-port-a-protocol-driver-to-ndis-6-20.md)と移植のサマリー ミニポート ドライバー[の概要。ポートの NDIS 6.20 が動作するためのミニポート ドライバーに必要な変更](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)します。

-   Windows 7 の後に、Microsoft Windows のバージョンでこの NDIS 5.x の中間フィルター ドライバーはサポートされません。 すべてのフィルター ドライバー、NDIS フィルター ドライバー インターフェイスを使用する必要があります。 NDIS フィルター ドライバーの詳細については、次を参照してください。[概要の変更に必要なポートの NDIS 6.20 が動作するためのフィルター ドライバー](summary-of-changes-required-to-port-a-filter-driver-to-ndis-6-20.md)します。

 

 





