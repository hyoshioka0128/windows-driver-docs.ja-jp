---
title: UMDF ドライバーでのアイドル電源切断のサポート
description: UMDF ドライバーでのアイドル電源切断のサポート
ms.assetid: 128f009e-1847-493e-90e3-2fe8c141b158
keywords:
- 電源管理 WDK UMDF、アイドル状態の電源切断
- アイドル状態の電源切断 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b2273b11f713dd2d292aa2049d23455019ebab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368648"
---
# <a name="supporting-idle-power-down-in-umdf-drivers"></a>UMDF ドライバーでのアイドル電源切断のサポート


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一部のデバイスは、システムでの稼働状態のまま、スリープ状態を入力できます。 このようなデバイスでは、フレームワークを開始する、デバイスがアイドル状態 (未使用) 後に、デバイスの電源を下げるの事前に定義された (および設定可能な) 時間に対して。

外部イベントを検出すると、バスのウェイク アップの信号をトリガーこれらのデバイスのこともできます。 バス ドライバーが、このシグナルに応答し、ドライバー スタック、デバイスを動作状態に復元します。 (外部イベントを検出しないデバイスまで低電力状態でフレームワークを稼働状態に、デバイスの復元を開始するバス ドライバーの確認です。)

アイドル状態のとき、デバイスを電源する場合、[電源ポリシー所有者](power-policy-ownership-in-umdf.md)次の 2 つの手順を実行する必要があります。

1.  呼び出す[ **IWDFDevice2::AssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)または[ **IWDFDevice3::AssignS0IdleSettingsEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)を指定します。
    -   デバイスが入力する低電力状態
    -   時間の電源状態が低くしたりする前に、デバイスをアイドル状態に残す必要があります。
    -   デバイスの外部のイベントの検出し、バスのウェイク アップの信号をトリガーできるかどうか
    -   ユーザーがデバイスのアイドル状態の設定を制御できるかどうか
    -   かどうか、フレームワークに配置できますデバイス D3cold 電源の状態、アイドル タイムアウト期間が切れるときに

    呼び出すことができます、ドライバーのバージョン 1.11 以降のフレームワークで作成した場合、 **IWDFDevice3::AssignS0IdleSettingsEx**の代わりに**IWDFDevice2::AssignS0IdleSettings**します。 上記の機能だけでなく**IWDFDevice3::AssignS0IdleSettingsEx**ドライバーを指定できます。
    -   アイドル状態のデバイスの電源機能を有効または無効にするかどうか
    -   作業 (S0) 状態に戻ると、システムにデバイスが作業 (D0) 状態に戻すかどうか

2.  実装、 [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)インターフェイスと次イベント コールバック関数、デバイスの必要な場合。
    -   [**IPowerPolicyCallbackWakeFromS0::OnArmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)、ウェイク アップの外部イベントに応答するデバイスのハードウェア (バスではない) ことができます。
    -   [**IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)、ウェイク アップの外部イベントに応答するデバイスの機能 (バスの機能ではない) を無効にします。
    -   [**IPowerPolicyCallbackWakeFromS0::OnWakeFromS0Triggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onwakefroms0triggered)バスがウェイク信号を検出、ドライバーに通知します。




フレームワークは、アイドル状態になるデバイスを考慮しの次の条件がすべて満たされたときに、アイドル時間をカウントします。

-   このデバイス インスタンス用に作成された電源管理対象のキューのいずれも任意の要求をキューで待機しているまたはドライバーにディスパッチします。 場合は、要求は、ドライバーにディスパッチされましたが、ドライバーが I/O のターゲットに送信、要求がキューにも関連して、デバイスがないと見なされるアイドル状態です。 電源に管理されていないキュー内の要求はカウントされませんデバイスに向けたアイドル状態。
-   ドライバーと呼ばれていた場合[ **IWDFDevice2::StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)、ドライバーは、その後、呼び出されて[ **IWDFDevice2::ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)します。
-   電源ポリシーの所有者がバス ドライバーの場合は、D0 ではありません、バス ドライバーの子デバイスです。

場合は、ドライバー (またはユーザー) には、アイドル状態に、デバイスの電源オフができますが、使用する必要があります、 [ **IWDFDevice2::StopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)メソッド。 デバイスがその動作 (D0) 状態の場合は、このメソッドは、ドライバー呼び出されるまでアイドル状態から、デバイスを防ぎます[ **IWDFDevice2::ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)します。 ドライバーを呼び出すときに、デバイスが省電力状態がかどうか**IWDFDevice2::StopIdle**フレームワークがデバイスの作業 (D0) 状態を復元するバス ドライバーを要求、システムが作業 (S0) の状態である場合と。 詳細については、ドライバーが呼び出す必要があります**IWDFDevice2::StopIdle**メソッドのリファレンス ページを参照してください。

低電力状態からスリープ解除できるデバイスの場合、デバイスのバスのドライバーは、デバイスの起動時に参加します。 カーネル モードのバス ドライバーでは、バス アダプターを有効にして、低電力状態から復帰するデバイスの機能を無効にするのに必要なことすべてを実行します。

デバイスのアイドル状態の機能を制御するレジストリ エントリについては、次を参照してください。[ユーザー コントロールのデバイス アイドル状態と UMDF Wake 動作](user-control-of-device-idle-and-wake-behavior-in-umdf.md)します。

 

 





