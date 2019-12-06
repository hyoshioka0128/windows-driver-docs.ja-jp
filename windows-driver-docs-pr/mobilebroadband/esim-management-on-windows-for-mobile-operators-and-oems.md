---
title: 通信事業者および OEM の Windows での eSIM 管理
description: 通信事業者および OEM の Windows での eSIM 管理
ms.assetid: 7D37D297-76FD-46DA-ACC3-73E4BF970524
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: bb1165868de85b98dec352c19ec5c148c85dabc1
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862867"
---
# <a name="esim-management-on-windows-for-mobile-operators-and-oems"></a>通信事業者および OEM の Windows での eSIM 管理

## <a name="mobile-operators-and-oems"></a>携帯電話および Oem

モバイルオペレーターまたは OEM で、Windows での eSIM 管理をサポートする場合は、次の手順を実行します。

1. ハードウェアラボキット (HLK) のテストの実行を実施します。 これにより、Windows 10 の eSIM サポートとのモデムハードウェアの互換性が確保されます。 Oem と Odm は、次の HLK eSIM テストを確実に実行する必要があります。
    1. 基本的な eSIM サポートテストケース:
        - [Win6_4.MB.CDMA.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/windows-hardware/test/hlk/testref/f27c8d81-7e2b-49d1-be4c-614bf62f003c)
        - [Win6_4.MB.GSM.Data.TestLowLevelUiccAccess](https://docs.microsoft.com/windows-hardware/test/hlk/testref/104db926-5cc4-47ad-a7d0-ff476b0f57a1)
    2. リムーバブル SIM スロットとはんだ eUICC の両方を備えた Windows 10 デバイスの場合:
        - [WIN6_4 MB。CDMA.Data. TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/049a0532-3d58-49aa-ac3d-2a9b8aab24a7)および/または[Win6_4 MB。GSM.Data. TestSlot](https://docs.microsoft.com/windows-hardware/test/hlk/testref/defddebe-cc40-4d6f-9b0c-ca5ca9a1cb4d)
        - [WIN6_4 MB。CDMA.Data. TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e4ec5199-0841-4864-ac17-b6b71f81cdf3)および/または[Win6_4 MB。GSM.Data. TestDeviceCapsEx](https://docs.microsoft.com/windows-hardware/test/hlk/testref/75c812d5-8c7d-4589-8336-7d72f2feb987)

Windows には、エンタープライズユースケースで、モバイルデバイス管理プロバイダーが eSIM プロファイルを管理する機能が用意されています。 ただし、Windows では、エコシステムパートナーがパートナーや顧客にこれを提供する方法は制限されていません。 そのため、Windows OMA-URI との統合によって、eSIM プロファイル管理機能をサポートできます。 これにより、会社のポリシーに従って eSIM プロファイルをリモートで管理できるようになります。

1つの MDM プロバイダーのみを統合して使用する場合は、そのプロバイダーに直接問い合わせてください。 さまざまな MDM プロバイダーを使用しているお客様に対して eSIM 管理を提供する場合は、 [orchestrator プロバイダー](https://www.idemia.com/esim-management-facilitation)にお問い合わせください。 Orchestrator プロバイダーは、MDM オンボードだけでなく、携帯電話会社のオンボードを処理するプロキシとして機能します。 これらの[役割](https://www.idemia.com/smart-connect-hub)は、すべてのパーティに対してプロセスを可能な限り簡単かつスケーラブルにすることです。

## <a name="esim-management-for-other-audiences"></a>他のユーザーのための eSIM 管理

MDM プロバイダーで、Windows での eSIM 管理をサポートする場合は、「[モバイルデバイス管理プロバイダーが windows での Esim 管理をサポートする方法](https://docs.microsoft.com/windows/client-management/mdm/esim-enterprise-management)」を参照してください。

組織のエンドユーザーであり、組織が提供するデバイスで携帯データネットワーク接続用の eSIM を使用する場合は、「 [Windows 10 PC で esim を使用して携帯データネットワーク接続を取得](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)する」を参照してください。