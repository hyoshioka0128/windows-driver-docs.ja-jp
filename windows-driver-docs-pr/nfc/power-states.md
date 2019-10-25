---
title: 電源の状態
description: NFC クラス拡張ドライバーは、デバイスの電源ポリシー所有者として機能します。そのため、デバイス初期化ルーチンで WdfDeviceInitSetPowerPolicyOwnership (TRUE) を呼び出します。
ms.assetid: 12433344-9C33-415B-BA14-4BD4C7E838CC
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1ad8e01cd57727a295f4937d180436d6f1a70c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834039"
---
# <a name="power-states"></a>電源の状態


NFC クラス拡張ドライバーは、デバイスの電源ポリシー所有者として機能します。そのため、デバイス初期化ルーチンで[**Wdfdeviceinitsetpowerpolicyownership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)(TRUE) を呼び出します。

NFC CX ドライバーは、デバイスの電源状態の D0 および D3 をサポートしています。 次の状態図は、2つの電源状態間の遷移を示しています。 アイドル状態のデバイスは、NFCC に電力がない D3 の電力状態にあります。 ラジオモードがアクティブであり、NFP (有効なパブリケーションまたは NFP DDI からのサブスクリプション) などのモジュール、SE (アクティブなセキュリティで保護されている、NFCSE DDI)、スマートカードがアクティブになっている場合、状態は D0 に遷移します。 この移行中、デバイスのポーリング状態は、すべてのアクティブモジュールの要件を満たすように更新されます。

![電源の状態](images/powerstate.png)

さらに、UMDF の組み込みのアイドル検出ロジックは、デバイスの電源管理に使用されます。 初期化中に、WdfDevice には次のように S0 Idle 設定が割り当てられます。

```cpp
WdfDeviceAssignS0IdleSettings(
    IdleCannotWakeFromS0,
    PowerDeviceD3,
    IdleTimeout,
    IdleAllowUserControl,
    WdfUseDefault
);
```

IdleTimeout の既定値は1秒です。 この設定は、 [**NFC\_CX\_クライアント\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)の*poweridletimeout*パラメーターを使用して構成できます。 次の状態図は、WDF idle detection メソッドの使用によって暗黙的に示されるさまざまな電源遷移を示しています。

クライアントドライバーは、 [**NFC\_CX\_クライアント\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ns-nfccx-_nfc_cx_client_config)構造体の**Ispowerpolicyowner**メンバーを介して、スタックの電源ポリシー所有者として選択できます。 これは、追加のデバイスの電源状態を構成する必要がある USB などのトランスポートに便利な場合があります。

![電源管理操作](images/powermanagementoperations.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

