---
title: SetTunnelModeOuterAddress
description: SetTunnelModeOuterAddress
ms.assetid: 0f67a15c-5077-460a-923c-8d86cc79a1bb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b339a44e37ef94b1a7fc6482c8df593ff4f8002b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580598"
---
# <a name="settunnelmodeouteraddress"></a>SetTunnelModeOuterAddress


**SetTunnelModeOuterAddress**で HBA イニシエーター ポートを使用するトンネル モードの外部アドレスを指定する管理アプリケーションを使用します。

トンネル モードでは、内部で暗号化された IP パケットはセキュリティ ゲートウェイのアドレスを含む外部の IP パケット内で入れ子にします。 **SetTunnelModeOuterAddress**メソッドを指定されたポートを通過する IP パケットに関連付けられているセキュリティ ゲートウェイのアドレスを示すために、管理アプリケーションを使用します。

HBA イニシエーターまたは HBA ミニポート ドライバーでが保持既定トンネル モードの外部アドレス不揮発性記憶域の不揮発性ストレージが使用可能な場合

**SetTunnelModeOuterAddress** 、パブリッシュされていないに属している[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **SetTunnelModeOuterAddress**メソッドのメンバーの説明を参照してください、 [ **SetTunnelModeOuterAddress\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff566187)と[ **SetTunnelModeOuterAddress\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566190)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_SecurityConfigOperations WMI クラスをサポートする必要があります**SetTunnelModeOuterAddress**します。

 

 





