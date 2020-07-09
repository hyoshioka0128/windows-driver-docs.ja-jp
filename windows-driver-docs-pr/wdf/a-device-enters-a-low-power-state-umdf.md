---
title: デバイスが低電力状態になる (UMDF 1)
description: デバイスが低電力状態になる
ms.assetid: c3697272-75ec-4de5-b123-3d1c68d2044e
keywords:
- 電源管理のシナリオ WDK UMDF、低電力状態への移行
- 低電力状態シナリオの WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1f6b0da890cb42d28b49a7b60c046151d331c6
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141259"
---
# <a name="a-device-enters-a-low-power-state-umdf-1"></a>デバイスが低電力状態になる (UMDF 1)


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次のいずれかが発生すると、デバイスは動作中 (D0) 状態を維持し、低電力状態になります。

-   デバイスはアイドル状態 (つまり、アクセスされていません) であり、システムが動作中 (S0) 状態のままになっている間は、低電力アイドル状態に入ることができます。

-   システムの電源状態が動作中 (S0) から低電力状態に変わりました。 (ドライバーは[**IWDFDevice2:: GetSystemPowerAction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-getsystempoweraction)を呼び出して、システムの電源状態が変更された理由を判断できます)。

デバイスをサポートする各 UMDF ベースの関数とフィルタードライバーについて、フレームワークは、ドライバースタックの最上位にあるドライバーから、一度に1つずつ、次の処理を実行します。

1.  ドライバーが自己管理型 i/o を使用している場合、フレームワークは、ドライバーの[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoSuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediosuspend)コールバック関数を呼び出します。

2.  フレームワークは、デバイスのすべての電源管理 i/o キューを停止し、 [**IPnpCallbackSelfManagedIo:: OnSelfManagedIoStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediostop)コールバック関数を呼び出します (存在する場合)。

3.  ドライバーがデバイスの電源ポリシーの所有者である場合、フレームワークは[**IPowerPolicyCallbackWakeFromS0:: OnArmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-onarmwakefroms0)または[**IPowerPolicyCallbackWakeFromSx:: OnArmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-onarmwakefromsx) callback 関数を呼び出します。

4.  フレームワークは、ドライバーの[**IPnpCallback:: OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit) callback 関数 (存在する場合) を呼び出します。

これらの手順を示す図を表示するには、[ユーザーがデバイスを Unplugs](a-user-unplugs-a-device.md)していることを確認してください。

 

 





