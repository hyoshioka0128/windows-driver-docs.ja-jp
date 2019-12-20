---
title: UMDF ドライバーでのシステム ウェイクアップのサポート
description: UMDF ドライバーでのシステム ウェイクアップのサポート
ms.assetid: 945b1751-f3a1-4a29-8fb7-6690f91af7d9
keywords:
- 電源管理 WDK UMDF、システムウェイクアップ
- システムウェイクアップ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7397965fce7c1774300af8c0372b4f8e4dcefe38
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210835"
---
# <a name="supporting-system-wake-up-in-umdf-drivers"></a>UMDF ドライバーでのシステム ウェイクアップのサポート


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

システムが低電力状態にある間、一部のデバイスでは、受信ネットワークパケットなどの外部イベントを検出し、システムをスリープ解除できます。 たとえば、デバイスの電源管理機能 (PMC) の登録に示されているように、PCI デバイスにシステムウェイクアップ機能がある場合、PCI バスの電源管理イベント (PME) シグナルを発生させてシステムをスリープ解除します。

デバイスがシステム全体の低電力状態からシステムをウェイクアップできる場合、[電源ポリシー所有者](power-policy-ownership-in-umdf.md)の[**Idriverentry:: ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数は、次の2つの手順を実行する必要があります。

1.  [**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)を呼び出して、以下を指定します。
    -   デバイスが入力する低電力状態
    -   ユーザーがデバイスのアイドル設定を制御できるかどうか
    -   デバイスのウェイク機能が有効か無効か

2.  デバイスに必要な場合は、 [IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)インターフェイスと次のイベントコールバック関数を実装します。
    -   [**IPowerPolicyCallbackWakeFromSx:: OnArmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx)。これにより、デバイスのハードウェアが外部のウェイクアップイベントに応答できるようになります。
    -   [**IPowerPolicyCallbackWakeFromSx:: OnDisarmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx)。これにより、デバイスが外部ウェイクアップイベントに応答する機能が無効になります。
    -   [**IPowerPolicyCallbackWakeFromSx:: OnWakeFromSxTriggered**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onwakefromsxtriggered)。バスがウェイクアップ信号を検出したことをドライバーに通知します。

バスドライバーは、システムのウェイクアップにも参加します。 デバイスのバスのカーネルモードドライバーは、デバイスが低電力状態から復帰できるようにするために、バスアダプターで必要なものをすべて行います。

デバイスのウェイクアップ機能を制御するレジストリエントリの詳細については、「 [UMDF でのデバイスのアイドル状態とウェイク動作のユーザー制御](user-control-of-device-idle-and-wake-behavior-in-umdf.md)」を参照してください。

 

 





