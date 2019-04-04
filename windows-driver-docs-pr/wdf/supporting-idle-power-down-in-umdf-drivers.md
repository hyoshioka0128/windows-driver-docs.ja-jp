---
title: UMDF ドライバーでのアイドル電源切断のサポート
description: UMDF ドライバーでのアイドル電源切断のサポート
ms.assetid: 128f009e-1847-493e-90e3-2fe8c141b158
keywords:
- 電源管理 WDK UMDF、アイドル状態の電源切断
- アイドル状態の電源切断 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e787270c51b037c1512115e8a19e5eb8657d74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578111"
---
# <a name="supporting-idle-power-down-in-umdf-drivers"></a>UMDF ドライバーでのアイドル電源切断のサポート


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一部のデバイスは、システムでの稼働状態のまま、スリープ状態を入力できます。 このようなデバイスでは、フレームワークを開始する、デバイスがアイドル状態 (未使用) 後に、デバイスの電源を下げるの事前に定義された (および設定可能な) 時間に対して。

外部イベントを検出すると、バスのウェイク アップの信号をトリガーこれらのデバイスのこともできます。 バス ドライバーが、このシグナルに応答し、ドライバー スタック、デバイスを動作状態に復元します。 (外部イベントを検出しないデバイスまで低電力状態でフレームワークを稼働状態に、デバイスの復元を開始するバス ドライバーの確認です。)

アイドル状態のとき、デバイスを電源する場合、[電源ポリシー所有者](power-policy-ownership-in-umdf.md)次の 2 つの手順を実行する必要があります。

1.  呼び出す[ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920)または[ **IWDFDevice3::AssignS0IdleSettingsEx** ](https://msdn.microsoft.com/library/windows/hardware/hh451202)を指定します。
    -   デバイスが入力する低電力状態
    -   時間の電源状態が低くしたりする前に、デバイスをアイドル状態に残す必要があります。
    -   デバイスの外部のイベントの検出し、バスのウェイク アップの信号をトリガーできるかどうか
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   かどうか、フレームワークに配置できますデバイス D3cold 電源の状態、アイドル タイムアウト期間が切れるときに

    呼び出すことができます、ドライバーのバージョン 1.11 以降のフレームワークで作成した場合、 **IWDFDevice3::AssignS0IdleSettingsEx**の代わりに**IWDFDevice2::AssignS0IdleSettings**します。 上記の機能だけでなく**IWDFDevice3::AssignS0IdleSettingsEx**ドライバーを指定できます。
    -   アイドル状態のデバイスの電源機能を有効または無効にするかどうか
    -   作業 (S0) 状態に戻ると、システムにデバイスが作業 (D0) 状態に戻すかどうか

2.  実装、 [IPowerPolicyCallbackWakeFromS0](https://msdn.microsoft.com/library/windows/hardware/ff556815)インターフェイスと次イベント コールバック関数、デバイスの必要な場合。
    -   [**IPowerPolicyCallbackWakeFromS0::OnArmWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff556817)、ウェイク アップの外部イベントに応答するデバイスのハードウェア (バスではない) ことができます。
    -   [**IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff556819)、ウェイク アップの外部イベントに応答するデバイスの機能 (バスの機能ではない) を無効にします。
    -   [**IPowerPolicyCallbackWakeFromS0::OnWakeFromS0Triggered**](https://msdn.microsoft.com/library/windows/hardware/ff556822)バスがウェイク信号を検出、ドライバーに通知します。




フレームワークは、アイドル状態になるデバイスを考慮しの次の条件がすべて満たされたときに、アイドル時間をカウントします。

-   このデバイス インスタンス用に作成された電源管理対象のキューのいずれも任意の要求をキューで待機しているまたはドライバーにディスパッチします。 場合は、要求は、ドライバーにディスパッチされましたが、ドライバーが I/O のターゲットに送信、要求がキューにも関連して、デバイスがないと見なされるアイドル状態です。 電源に管理されていないキュー内の要求はカウントされませんデバイスに向けたアイドル状態。
-   ドライバーと呼ばれていた場合[ **IWDFDevice2::StopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff556948)、ドライバーは、その後、呼び出されて[ **IWDFDevice2::ResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff556943)します。
-   電源ポリシーの所有者がバス ドライバーの場合は、D0 ではありません、バス ドライバーの子デバイスです。

場合は、ドライバー (またはユーザー) には、アイドル状態に、デバイスの電源オフができますが、使用する必要があります、 [ **IWDFDevice2::StopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff556948)メソッド。 デバイスがその動作 (D0) 状態の場合は、このメソッドは、ドライバー呼び出されるまでアイドル状態から、デバイスを防ぎます[ **IWDFDevice2::ResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff556943)します。 ドライバーを呼び出すときに、デバイスが省電力状態がかどうか**IWDFDevice2::StopIdle**フレームワークがデバイスの作業 (D0) 状態を復元するバス ドライバーを要求、システムが作業 (S0) の状態である場合と。 詳細については、ドライバーが呼び出す必要があります**IWDFDevice2::StopIdle**メソッドのリファレンス ページを参照してください。

低電力状態からスリープ解除できるデバイスの場合、デバイスのバスのドライバーは、デバイスの起動時に参加します。 カーネル モードのバス ドライバーでは、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

デバイスのアイドル状態の機能を制御するレジストリ エントリについては、[ユーザー コントロールのデバイス アイドル状態と UMDF Wake 動作](user-control-of-device-idle-and-wake-behavior-in-umdf.md)を参照してください。

 

 





