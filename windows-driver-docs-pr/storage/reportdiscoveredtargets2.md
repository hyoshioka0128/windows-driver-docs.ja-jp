---
title: ReportDiscoveredTargets2
description: ReportDiscoveredTargets2
ms.assetid: 2845cfa9-a85c-45d4-a962-8f409e96ccec
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dbd9f1c3018cd892520ece639ab9c5ef88a40946
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842696"
---
# <a name="reportdiscoveredtargets2"></a>ReportDiscoveredTargets2


**ReportDiscoveredTargets2** WMI メソッドは、検出されたすべてのターゲットを報告します。

この WMI メソッドは、「 *Discover .mof*」で定義されている、公開されていない[Msiscsi\_discoveryoperations WMI クラス](msiscsi-discoveryoperations-wmi-class.md)に属しています。 **ReportDiscoveredTargets2**メソッドのパラメーターの説明については、 [**ReportDiscoveredTargets2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsifnd/ns-iscsifnd-_reportdiscoveredtargets2_out)構造体のメンバーの説明を参照してください。

**ReportDiscoveredTargets2**は[ReportDiscoveredTargets](reportdiscoveredtargets.md)メソッドに似ていますが、 **ReportDiscoveredTargets2**は**ReportDiscoveredTargets**メソッドによって報告されないターゲットポータル情報 (タグなど) を報告します。ポータルグループの番号。

MSiSCSI\_DiscoveryOperations WMI クラスを実装するミニポートドライバーは、 **ReportDiscoveredTargets2**をサポートしている必要があります。

 

 





