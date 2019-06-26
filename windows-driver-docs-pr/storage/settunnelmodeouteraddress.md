---
title: SetTunnelModeOuterAddress
description: SetTunnelModeOuterAddress
ms.assetid: 0f67a15c-5077-460a-923c-8d86cc79a1bb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2bbfa2e1a86ec308bc38eda1f24835067077a025
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369558"
---
# <a name="settunnelmodeouteraddress"></a>SetTunnelModeOuterAddress


**SetTunnelModeOuterAddress**で HBA イニシエーター ポートを使用するトンネル モードの外部アドレスを指定する管理アプリケーションを使用します。

トンネル モードでは、内部で暗号化された IP パケットはセキュリティ ゲートウェイのアドレスを含む外部の IP パケット内で入れ子にします。 **SetTunnelModeOuterAddress**メソッドを指定されたポートを通過する IP パケットに関連付けられているセキュリティ ゲートウェイのアドレスを示すために、管理アプリケーションを使用します。

HBA イニシエーターまたは HBA ミニポート ドライバーでが保持既定トンネル モードの外部アドレス不揮発性記憶域の不揮発性ストレージが使用可能な場合

**SetTunnelModeOuterAddress** 、パブリッシュされていないに属している[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **SetTunnelModeOuterAddress**メソッドのメンバーの説明を参照してください、 [ **SetTunnelModeOuterAddress\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_in)と[ **SetTunnelModeOuterAddress\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_out)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_SecurityConfigOperations WMI クラスをサポートする必要があります**SetTunnelModeOuterAddress**します。

 

 





