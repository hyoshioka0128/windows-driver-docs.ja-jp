---
title: デバイスの電源切断
description: デバイスの電源切断
ms.assetid: d2525e15-9590-4fc0-955c-ca3540c13375
keywords:
- デバイスの電源ダウン WDK カーネル
- WDK カーネルのデバイスの電源
- IRP_MN_REMOVE_DEVICE
- WDK 電源管理のデバイスをオフにします。
- 自動電源ダウン WDK カーネル
- シャット ダウンの電源管理の WDK カーネル
- WDK のカーネルを電源オフ
- Irp WDK の電源管理
- 突然削除 WDK の電源管理
- デバイス削除 WDK の電源管理
- デバイスの削除
- I/O WDK 電源管理
- 予期しないデバイスの削除の WDK 電源管理
- アイドル状態検出 WDK 電源管理
- WDK カーネルの電源を節約します。
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91053c853868ea8bc43347fd855472fbb508aa59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572571"
---
# <a name="powering-down-a-device"></a>デバイスの電源切断





ウェイク アップでデバイスを有効にしない限り、そのドライバー電源をオフ、システムのシャット ダウン時。 デバイスの削除または突然の削除時にオフ電源常にする必要があります。

デバイスが削除されるときに、プラグ アンド プレイ マネージャに送信、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)デバイス スタックを要求します。 この IRP への応答、デバイスのドライバーがいることを確認デバイスの電源ダウン。 削除処理の暗黙の部分には、デバイスの電源デバイスの電源ポリシー所有者は、送信する必要はありません、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)の**PowerDeviceD3**します。

ドライバーの処理、 **IRP\_MN\_削除\_デバイス**要求、保留中の呼び出しを完了して、処理、任意の必要な削除を実行する I/O の待機[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765) D3、状態、デバイスが電源マネージャーに通知し、このデバイスの作成、デバイス オブジェクトを削除します。 通常、バス ドライバーは、デバイスの電源をオフにします。

デバイスは、Windows 2000 以降のオペレーティング システムから削除されるが予期せず、プラグ アンド プレイ manager 送信、 [ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)対応するデバイス スタックの一番上に要求します。 この IRP への応答、デバイスのドライバーする必要があります突然の削除、処理を実行」の説明に従って[IRP の処理\_MN\_突然\_削除要求](handling-an-irp-mn-surprise-removal-request.md)します。

システムのシャット ダウン、電源マネージャー送信、 **IRP\_MN\_設定\_POWER**システム電源の状態 (S4 または S5)。 デバイスの電源ポリシー所有者は、この IRP を受信するときに送信する必要があります、 **IRP\_MN\_設定\_POWER**の**PowerDeviceD3**下位のドライバーを終了できるように、職場と電力は、デバイスをダウンします。

ドライバーは、そのデバイスのアイドル状態の検出を実行できます必要に応じてまたはデバイス電源を切断できる場合に使用中でないように電源マネージャーがアイドル状態の検出を実行することを要求できます。 詳細については、次を参照してください。 [、アイドル状態のデバイスを検出する](detecting-an-idle-device.md)します。

 

 




