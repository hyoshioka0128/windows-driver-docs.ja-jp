---
title: デバイスを停止する要求の処理
description: デバイスを停止する要求の処理
ms.assetid: 4c8f37b3-7961-4c78-a88b-3eec58155e66
keywords:
- PnP WDK KMDF、デバイスを停止しています
- プラグ アンド プレイ WDK KMDF、デバイスを停止しています
- WDK KMDF のリソースを再配布
- リソースの再配布 WDK KMDF
- WDK KMDF のデバイスを削除します。
- WDK KMDF とデバイスの停止要求
- WKD KMDF、PnP とデバイスの停止要求
- デバイスの一時停止 WDK KMDF
- デバイスの一時停止 WDK KMDF、PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3bc2b67b1e68ed78850175f0aa53cb15f0f0c61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550656"
---
# <a name="handling-requests-to-stop-a-device"></a>デバイスを停止する要求の処理


これには、デバイスを停止するデバイスのドライバーを要求する前に、PnP、上司からドライバーをお勧めは、デバイスを停止するかどうか、2 つの状況があります。

-   新しいデバイスをユーザーが接続され、PnP マネージャーである必要があります[システムのハードウェア リソースを再配布](#redistributing-resources)新しいデバイスを対応するためにします。

-   そのユーザーには、ユーザーが示されて[デバイスを削除](#a-user-removes-or-disables-a-device)します。

ドライバーがこのような状況を処理できるいくつかの方法はあります。

-   ドライバーが呼び出された場合[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)デバイスは特別なファイルをサポートしていると、特別なファイルが開いて、デバイスの場合、フレームワークは停止するデバイスを許可しないため、.

-   比較的短時間に一時的にすべての中断を防ぐためには、ドライバーを呼び出すことができます[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)します。

-   評価を停止が試行されるたびに個別に処理は、ドライバーが提供できる[ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)と[ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)コールバック関数。

場合は、デバイスは、特別なファイルをサポートしていないと、ドライバーが提供しない停止やデバイスを削除することは、ドライバーまたはデバイスの問題ありません場合、 *EvtDeviceQueryStop*と*EvtDeviceQueryRemove*コールバック関数し、呼び出すことはありません**WdfDeviceSetStaticStopRemove**します。 ここでは PnP マネージャーは、そのドライバーを使用できるかどうかに最初に確認、デバイスを常に停止します。

### <a href="" id="redistributing-resources"></a> リソースの再配布

場合があります、PnP マネージャーは、システムのハードウェア リソースを再配布する必要があります。 通常、この再配布は、バス ドライバーとことで、新しいデバイスが取り込まれていて、新しいデバイスが既に割り当てられているリソースが必要ですが報告されたために発生します。 リソースの再割り当てする前に、デバイスを停止する必要があります。

ドライバーが提供できる、ビジー状態のデバイスを停止することがありますように PnP マネージャーは、ドライバーの必要がある場合、 [ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)コールバック関数。 場合、ドライバーの*EvtDeviceQueryStop*コールバック関数がエラー状態値を返します、PnP マネージャーでは、デバイスは停止されません。

コールバック関数が状態を返す場合は、ドライバーは、デバイスを停止しても安全であるかを決定します、\_成功します。 その他のデバイスの場合は、ドライバーの中断を防ぐため、PnP マネージャーは、デバイスを一時的に停止します。

フレームワーク ドライバーのイベントのコールバック関数、PnP マネージャーがリソースを再配布するデバイスを停止したときの順序の詳細については、[PnP マネージャーでは再配布システム Resources](the-pnp-manager-redistributes-system-resources.md)を参照してください。

### <a href="" id="a-user-removes-or-disables-a-device"></a> ユーザーが削除またはデバイスを無効にします

ユーザーでは、削除したり、一部のデバイスを無効にすることができます。 次に、例を示します。

-   ドライバーを設定した場合、**リムーバブル**メンバー (および not、 **SurpriseRemovalOK**メンバー) のデバイスの[ **WDF\_デバイス\_PNP\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551257)構造体には、ユーザーことができます取り外しますプログラムを実行し、取り外す、または取り出すデバイス。

-   ドライバーが設定されていない場合、 **NotDisableable**のデバイスのメンバー [ **WDF\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff551284)構造体には、ユーザーがデバイスを使用できますデバイスを無効にするマネージャー。

このような場合、PnP マネージャーは、ユーザーが削除する前にデバイスを停止しようとします。

ドライバーが提供できる場合があります、ビジー状態のデバイスの削除を防ぐために、ドライバーに必要な場合は、 [ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)コールバック関数。 場合、ドライバーの*EvtDeviceQueryRemove*コールバック関数がエラー状態値を返します、PnP マネージャーでは、デバイスは停止されません。

コールバック関数が状態を返す場合は、ドライバーは、デバイスを削除するユーザーに対しても安全であるかを決定します、\_成功します。 他のデバイスの場合は、ドライバーには、削除ができないように、PnP マネージャーは、デバイスを停止します。

フレームワーク ドライバーのイベントのコールバック関数の削除、デバイスを停止するときに順序については、[ユーザーがデバイスから切り離し](a-user-unplugs-a-device.md)を参照してください。

 

 





