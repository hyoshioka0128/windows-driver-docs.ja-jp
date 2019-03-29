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
ms.openlocfilehash: ba7bc388e9530e90d0d3771c51920841f4fa1b1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580490"
---
# <a name="introduction-to-wdm"></a>WDM の概要


開発者がソース コードと互換性のあるすべての Microsoft Windows で動作しているシステムでは、デバイス ドライバーを記述する、 *Windows Driver Model* (WDM) が導入されました。 WDM 規則に従うカーネル モード ドライバーが呼び出されて*WDM ドライバー*します。




すべて WDM ドライバーでは、次の操作を行う必要があります。

-   Wdm.h、いない Ntddk.h が含まれます。 (Wdm.h Ntddk.h のサブセットであることに注意してください)。

-   」の説明に従って、バス ドライバー、関数ドライバー、または、フィルター ドライバーとして設計する[WDM ドライバーの種類](types-of-wdm-drivers.md)します。

-   デバイス オブジェクトを作成する」の説明に従って[WDM デバイス オブジェクトとデバイス スタック](wdm-device-objects-and-device-stacks.md)します。

-   サポート[プラグ アンド プレイ (PnP)](implementing-plug-and-play.md)します。

-   サポート[電源管理](implementing-power-management.md)します。

-   サポート[Windows Management Instrumentation](implementing-wmi.md) (WMI)。

### <a name="does-the-wdk-cover-non-wdm-drivers"></a>WDK カバー非 WDM ドライバーのでしょうか

Windows Driver Kit (WDK) には、カーネル モードの WDM ドライバーの開発が強調されていますが、WDK には、WDM 規則に従っていないカーネル モード ドライバーに関連する情報も含まれています。 この情報により、既存の非 WDM ドライバーを維持するために、新しいドライバーにこれらの既存のドライバーとそのインターフェイスを記述します。

### <a name="should-you-always-write-a-wdm-driver"></a>常に WDM ドライバーを記述する必要がありますか。

新しいカーネル モード ドライバーを作成する場合、WDM ドライバーがあります*しない限り、* 非 WDM ドライバーのスタックに挿入されるドライバーを作成します。 新しいドライバーを決定するデバイスの種類に固有 Microsoft が提供ドライバーのドキュメントを Microsoft から提供されたドライバーとやり取りする必要がありますお読みください。 デバイスの種類に固有の詳細については、次を参照してください[デバイスとドライバー テクノロジ](https://msdn.microsoft.com/library/windows/hardware/ff557557)。)。

**注**  WDM ドライバーのすべての新しいドライバー スタックがあります。

 

クロス プラットフォームの問題、考慮すべきは WDM または非 WDM ドライバーを開発しているかどうか。 詳細については、次を参照してください。[さまざまなバージョンの Windows のドライバーを書き込み](https://msdn.microsoft.com/library/windows/hardware/ff554887)します。

使用を検討する新しい WDM ドライバーを作成する場合もする必要があります、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/dn265580)(KMDF)。 KMDF は、WDM インターフェイスよりも簡単に使用されるインターフェイスを提供します。

 

 




