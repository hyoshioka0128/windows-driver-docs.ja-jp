---
title: Windows 上の携帯電話会社や Oem の eSIM 管理
description: Windows 上の携帯電話会社や Oem の eSIM 管理
ms.assetid: 7D37D297-76FD-46DA-ACC3-73E4BF970524
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82f14e695ad7973f560110f025a95e40d29038bb
ms.sourcegitcommit: 6152f92c5d2bc7c8db08dd0fdbc0146f88e8413b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66224507"
---
# <a name="esim-management-on-windows-for-mobile-operators-and-oems"></a>Windows 上の携帯電話会社や Oem の eSIM 管理

## <a name="mobile-operators-and-oems"></a>携帯電話会社や Oem

携帯電話会社や OEM、している Windows の eSIM の管理をサポートする場合は、これらの手順に従います。

1. ハードウェア ラボ キット (HLK) テストの実行を実行します。 これにより、Windows 10 の eSIM のサポートのモデム ハードウェアの互換性。 Oem、Odm 次 HLK eSIM テストの実行を確認する必要があります。
    1. Esim 状の基本的なサポートのテスト_ケース:
        - [Win6_4.MB.CDMA.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/windows-hardware/test/hlk/testref/f27c8d81-7e2b-49d1-be4c-614bf62f003c)
        - [Win6_4.MB.GSM.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/104db926-5cc4-47ad-a7d0-ff476b0f57a1)
    2. リムーバブル SIM スロットとはんだ eUICC の両方で Windows 10 デバイス。
        - [Win6_4.MB します。CDMA します。Data.TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/049a0532-3d58-49aa-ac3d-2a9b8aab24a7)や[Win6_4.MB します。GSM します。Data.TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/defddebe-cc40-4d6f-9b0c-ca5ca9a1cb4d)
        - [Win6_4.MB します。CDMA します。Data.TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e4ec5199-0841-4864-ac17-b6b71f81cdf3)や[Win6_4.MB します。GSM します。Data.TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/75c812d5-8c7d-4589-8336-7d72f2feb987)

Windows では、企業のユース ケースで eSIM プロファイルを管理するモバイル デバイス管理プロバイダーの機能を提供します。 ただし、Windows は制限されません、独自のパートナーや顧客に機能を提供するエコシステム パートナーが方法する可能性があります。 そのため、Windows OMA-DM とを統合することによって eSIM プロファイルの管理機能をサポートできます。 これにより、リモートで会社のポリシーに従って eSIM プロファイルを管理できるようにします。

1 つのみの MDM プロバイダーと統合して使用する場合は、直接そのプロバイダーに問い合わせてください。 Esim 状の管理を別の MDM プロバイダーにお問い合わせくださいを使用して顧客に提供したい場合、 [orchestrator プロバイダー](https://www.idemia.com/esim-management-facilitation)します。 Orchestrator のプロバイダーは、通信事業者のオンボードと MDM のオンボードを処理するプロキシとして機能します。 その[ロール](https://www.idemia.com/smart-connect-hub)簡単と可能な拡張性の高いすべての当事者に対して、プロセスを確保します。

## <a name="esim-management-for-other-audiences"></a>その他のユーザー向けの eSIM の管理

MDM プロバイダーを Windows の eSIM の管理をサポートする場合は、次を参照してください。[モバイル デバイス管理プロバイダー方法は、Windows の eSIM 管理をサポート](https://docs.microsoft.com/windows/client-management/mdm/esim-enterprise-management)します。

エンド ユーザーが組織であり、組織で提供されるデバイスの携帯データ ネットワーク接続、eSIM を使用する場合を参照してください。 [、eSIM を使用して、Windows 10 PC で携帯データ ネットワーク接続を取得する](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)します。