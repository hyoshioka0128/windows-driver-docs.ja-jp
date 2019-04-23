---
title: WDM の概要
description: デバイス ドライバーを書き込むことはすべての Microsoft Windows の間でソース コードと互換性のあるオペレーティング システムのドライバー開発者を許可するのには、Windows Driver Model (WDM) が導入されました。 WDM 規則に従うカーネル モード ドライバーでは、WDM ドライバーと呼ばれます。
ms.assetid: 00225ec6-fe56-4cbc-b94d-2ba5f28c0bb9
keywords:
- WDM WDK カーネル
- Windows Driver Model WDK カーネル
- WDM ドライバー WDK カーネル
- Wdm.h
- Ntddk.h
- WDM ドライバー WDK カーネル、WDM ドライバーについて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfaae90d1641d9def7fb833ba2e1166fd75c71c6
ms.sourcegitcommit: 6df760d981c019f160e1a0ba91fc0ea576db3278
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60159037"
---
# <a name="introduction-to-wdm"></a>WDM の概要

> [!NOTE]
> このセクションには、推奨されるドライバー モデルではなくなり、WDM ドライバーに関するガイダンスが含まれています。 ドライバー モデルを選択する方法の詳細については、次を参照してください。[ドライバー モデルを選択する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)します。

開発者がソース コードと互換性のあるすべての Microsoft Windows で動作しているシステムでは、デバイス ドライバーを記述する、 *Windows Driver Model* (WDM) が導入されました。 WDM 規則に従うカーネル モード ドライバーが呼び出されて*WDM ドライバー*します。

すべて WDM ドライバーでは、次の操作を行う必要があります。

-   Wdm.h、いない Ntddk.h が含まれます。 (Wdm.h Ntddk.h のサブセットであることに注意してください)。

-   」の説明に従って、バス ドライバー、関数ドライバー、または、フィルター ドライバーとして設計する[WDM ドライバーの種類](types-of-wdm-drivers.md)します。

-   デバイス オブジェクトを作成する」の説明に従って[WDM デバイス オブジェクトとデバイス スタック](wdm-device-objects-and-device-stacks.md)します。

-   サポート[プラグ アンド プレイ (PnP)](implementing-plug-and-play.md)します。

-   サポート[電源管理](implementing-power-management.md)します。

-   サポート[Windows Management Instrumentation](implementing-wmi.md) (WMI)。

### <a name="should-you-write-a-wdm-driver"></a>WDM ドライバーを作成する必要がありますか。

新しいドライバーを作成する場合は、使用を検討して、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/dn265580)(KMDF)。 KMDF は、WDM インターフェイスよりも簡単に使用されるインターフェイスを提供します。

書き込みません WDM ドライバー、ドライバーを非 WDM ドライバーのスタックに挿入されるかどうか。 新しいドライバーを決定するデバイスの種類に固有 Microsoft が提供ドライバーのドキュメントを Microsoft から提供されたドライバーとやり取りする必要がありますお読みください。 デバイスの種類に固有の詳細については、次を参照してください[デバイスとドライバー テクノロジ](https://msdn.microsoft.com/library/windows/hardware/ff557557)。)。



