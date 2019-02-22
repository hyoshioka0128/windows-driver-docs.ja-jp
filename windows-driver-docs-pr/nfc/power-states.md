---
title: 電源の状態
description: NFC クラスの拡張機能ドライバーは、中、デバイスの初期化ルーチンに WdfDeviceInitSetPowerPolicyOwnership(TRUE) を呼び出すために、デバイスの電源ポリシー所有者として機能します。
ms.assetid: 12433344-9C33-415B-BA14-4BD4C7E838CC
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7870bf343ed2870f3330124c5a4721727690426c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538170"
---
# <a name="power-states"></a>電源の状態


呼び出すために、NFC クラスの拡張機能ドライバーが、デバイスの電源ポリシーの所有者として機能[ **WdfDeviceInitSetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546776)(TRUE)、デバイスの初期化ルーチンの中にします。

NFC CX ドライバーには、D0 と D3 のデバイスの電源状態がサポートしています。 次の状態図は、2 つの電源状態の間の移行を示します。 アイドル状態のデバイスは、NFCC と電源が入っていません D3 電源の状態です。 ラジオ モードがアクティブなすべてのモジュール NFP (アクティブなパブリケーションまたはサブスクリプション NFP DDI から)、SE (NFCSE DDI からエミュレーション モードでのアクティブなセキュリティで保護された要素) またはスマート カードがアクティブななど、状態は、D0 に移行します。 この移行中にアクティブなすべてのモジュールの要件を満たすデバイスのポーリングの状態が更新されます。

![電源の状態](images/powerstate.png)

さらに、UMDF の組み込みのアイドル状態の検出ロジックは、マネージャー、デバイスの電源に使用されます。 初期化中に、WdfDevice に次のように S0 アイドル状態の設定が割り当てられます。

```cpp
WdfDeviceAssignS0IdleSettings(
    IdleCannotWakeFromS0,
    PowerDeviceD3,
    IdleTimeout,
    IdleAllowUserControl,
    WdfUseDefault
);
```

1 秒間にアイドル タイムアウトの既定値です。 この設定を使用して構成可能な*PowerIdleTimeout*パラメーター [ **NFC\_CX\_クライアント\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn905540)します。 次の状態図は、WDF のアイドル状態の検出方法を使用して暗黙的に指定されたさまざまな電源切り替え効果を示します。

上のスタックの電源ポリシー所有者にするクライアント ドライバーを選択できます、 **IsPowerPolicyOwner**のメンバー、 [ **NFC\_CX\_クライアント\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn905540)構造体。 これは、追加のデバイスの電源状態を構成する必要があります USB などのトランスポートの便利なことがあります。

![電源管理操作](images/powermanagementoperations.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

