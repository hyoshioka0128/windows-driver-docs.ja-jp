---
title: SetTunnelModeOuterAddress
description: SetTunnelModeOuterAddress
ms.assetid: 0f67a15c-5077-460a-923c-8d86cc79a1bb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2ae9f9f3d1dcec580694a633ba4d3904eb744e1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842606"
---
# <a name="settunnelmodeouteraddress"></a>SetTunnelModeOuterAddress


**SetTunnelModeOuterAddress**を使用すると、管理アプリケーションで、イニシエーター HBA でポートが使用するトンネルモードの外部アドレスを指定できます。

トンネルモードでは、内部で暗号化された IP パケットが、セキュリティゲートウェイのアドレスを含む外部 IP パケット内に入れ子になっています。 **SetTunnelModeOuterAddress**メソッドを使用すると、管理アプリケーションは、指定されたポートを通過する IP パケットに関連付けられているセキュリティゲートウェイのアドレスを示すことができます。

不揮発性記憶域が使用可能な場合、イニシエーター HBA または HBA ミニポートドライバーは、既定のトンネルモード外部アドレスを不揮発性ストレージに保持する必要があります。

**SetTunnelModeOuterAddress**は、発行されていない[Msiscsi\_SECURITYCONFIGOPERATIONS WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **SetTunnelModeOuterAddress**メソッドのパラメーターの説明については、「」および「 [**SetTunnelModeOuterAddress\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_out)構造体」の「メンバーの[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_in)説明」を参照してください。

MSiSCSI\_SecurityConfigOperations WMI クラスを実装するミニポートドライバーは、 **SetTunnelModeOuterAddress**をサポートしている必要があります。

 

 





