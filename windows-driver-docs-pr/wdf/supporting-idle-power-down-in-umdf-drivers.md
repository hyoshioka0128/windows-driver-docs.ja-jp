---
title: UMDF ドライバーでのアイドル電源切断のサポート
description: UMDF ドライバーでのアイドル電源切断のサポート
ms.assetid: 128f009e-1847-493e-90e3-2fe8c141b158
keywords:
- 電源管理 WDK UMDF、アイドル電力ダウン
- アイドル状態の非アクティブな WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e50c1eacf39891cf6607c8d360c8866dfabc4295
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210764"
---
# <a name="supporting-idle-power-down-in-umdf-drivers"></a>UMDF ドライバーでのアイドル電源切断のサポート


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

一部のデバイスは、システムの動作状態が維持されている間にスリープ状態になることがあります。 このようなデバイスでは、デバイスがアイドル状態 (使用されていない) になると、事前に決められた時間が経過すると、デバイスの電源が低下します。

これらのデバイスの中には、外部イベントを検出したときにバスでウェイクアップ信号をトリガーするものもあります。 バスドライバーはこの信号に応答し、ドライバースタックはデバイスを動作状態に復元します。 (外部イベントを検出しないデバイスは、その動作状態へのデバイスの復元を開始するようにバスドライバーに指示されるまで、低電力状態のままになります)。

アイドル状態のときにデバイスの電源を切ることができる場合、[電源ポリシーの所有者](power-policy-ownership-in-umdf.md)は次の2つの手順を実行する必要があります。

1.  [**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)または[**IWDFDevice3:: AssignS0IdleSettingsEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)を呼び出して、以下を指定します。
    -   デバイスが入力する低電力状態
    -   デバイスがアイドル状態のままになってから電力状態が減少するまでの時間
    -   デバイスが外部イベントを検出し、バスでウェイクアップシグナルをトリガーできるかどうか
    -   ユーザーがデバイスのアイドル設定を制御できるかどうか
    -   アイドルタイムアウト期間が経過したときに、フレームワークがデバイスを D3cold の電源状態にするかどうか

    ドライバーがバージョン1.11 以降のフレームワークでビルドされている場合は、 **IWDFDevice2:: AssignS0IdleSettings**の代わりに**IWDFDevice3:: AssignS0IdleSettingsEx**を呼び出すことができます。 **IWDFDevice3:: AssignS0IdleSettingsEx**では、上記の機能に加えて、ドライバーが次のものを指定できます。
    -   デバイスのアイドル状態の電源をオンまたはオフにするかどうか
    -   システムが動作中 (S0) 状態に戻ったときに、デバイスが動作中 (D0) 状態に戻るかどうか

2.  デバイスに必要な場合は、 [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)インターフェイスと次のイベントコールバック関数を実装します。
    -   [**IPowerPolicyCallbackWakeFromS0:: OnArmWakeFromS0。**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)これにより、バスではなくデバイスハードウェアが外部ウェイクアップイベントに応答できるようになります。
    -   [**IPowerPolicyCallbackWakeFromS0:: OnDisarmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)。外部ウェイクアップイベントに応答するためのデバイスの機能 (バスの機能ではない) を無効にします。
    -   [**IPowerPolicyCallbackWakeFromS0:: OnWakeFromS0Triggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onwakefroms0triggered)。バスがウェイクアップ信号を検出したことをドライバーに通知します。




次のすべての条件が満たされると、フレームワークはデバイスがアイドル状態であると見なし、アイドル時間のカウントを開始します。

-   このデバイスインスタンスに対して作成された電源管理キューには、キューで待機しているかドライバーにディスパッチされた要求がありません。 要求がドライバーにディスパッチされ、ドライバーから i/o ターゲットに送信された場合でも、要求はキューに関連付けられており、デバイスはアイドル状態と見なされません。 非電力管理キューの要求は、デバイスのアイドル状態に対してカウントされません。
-   ドライバーが以前に[**IWDFDevice2:: StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)を呼び出した場合、ドライバーは[**IWDFDevice2:: ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)という名前になります。
-   電源ポリシーの所有者がバスドライバーの場合、バスドライバーの子デバイスはいずれも D0 にありません。

お使いのデバイスでドライバー (またはユーザー) がアイドル状態の電源を入れている場合は、 [**IWDFDevice2:: StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)メソッドを使用することが必要になる場合があります。 デバイスが動作中 (D0) 状態の場合、このメソッドは、ドライバーが[**IWDFDevice2:: ResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-resumeidle)を呼び出すまで、デバイスがアイドル状態されないようにします。 ドライバーが**IWDFDevice2:: StopIdle**を呼び出したときにデバイスが低電力状態になっていて、システムが動作している (S0) 状態にある場合、フレームワークは、デバイスを動作 (D0) 状態に復元するようにバスドライバーに要求します。 ドライバーが**IWDFDevice2:: StopIdle**を呼び出す必要がある場合の詳細については、メソッドのリファレンスページを参照してください。

デバイスを低電力状態からスリープ解除できる場合、デバイスのバスのドライバーはデバイスのスリープ解除に参加します。 カーネルモードバスドライバーは、デバイスが低電力状態から復帰できるようにするために、バスアダプターで必要な機能をすべて備えています。

デバイスのアイドル状態を制御するレジストリエントリの詳細については、「 [UMDF でデバイスのアイドル状態とスリープ状態の動作を制御](user-control-of-device-idle-and-wake-behavior-in-umdf.md)する」を参照してください。

 

 





