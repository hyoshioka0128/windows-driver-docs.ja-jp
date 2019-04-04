---
title: デバイスの識別文字列
description: プラグ アンド プレイ (PnP) マネージャーとその他のデバイスのインストール コンポーネントは、コンピューターにインストールされているデバイスを識別するためにデバイスの識別文字列を使用します。
ms.assetid: dae23185-63d9-4a0f-9786-c7fa66368826
keywords:
- 互換性のある Id WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- デバイス インスタンス Id の WDK デバイスのインストール
- ドライバー ノード WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- インスタンス Id の WDK デバイスのインストール
- デバイス セットアップ WDK デバイスのインストール、デバイスの識別文字列
- デバイスのインストール WDK、デバイスの識別文字列
- デバイスの識別文字列、WDK のデバイスをインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8eb23f0e5429b26fff04f04c25d7e1135a7b4fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559379"
---
# <a name="device-identification-strings"></a>デバイスの識別文字列

プラグ アンド プレイ (PnP) マネージャー、およびその他の[デバイス インストール コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)コンピューターにインストールされているデバイスを識別するためにデバイスの識別文字列を使用します。

Windows では、次のデバイスの識別文字列を使用して、デバイスに最も一致する情報 (INF) ファイルを見つけます。 これらの文字列は、デバイスの列挙子、標準のプラグ アンド プレイ ハードウェアに基づいて PnP デバイスを検出するシステム コンポーネントによって報告されます。 これらのタスクは、PnP マネージャーとのパートナーシップで、、バス ドライバーの PnP によって保持されています。 デバイスは通常、PCI などの親バス ドライバーまたは PCMCIA バス ドライバーによって列挙されます。 ACPI ドライバーなどの bus フィルター ドライバーでは、一部のデバイスが列挙されます。

- [ハードウェア Id](hardware-ids.md)

- [互換性 Id](compatible-ids.md)

Windows では、ハードウェア Id または互換性 Id の 1 つの一致を見つけようとします。 Windows がこれらの Id を使用して、INF ファイルにデバイスを照合する方法と、INF ファイルで Id を指定する方法の詳細については、[Windows ドライバーを選択する方法](how-setup-selects-drivers.md)を参照してください。

上記の Id を使用して、デバイスを識別するために、だけでなく PnP マネージャーは次の Id を使用してコンピューターにインストールされている各デバイスのインスタンスを一意に識別します。

- [インスタンス Id](instance-ids.md)

- [デバイス インスタンス Id](device-instance-ids.md)

Windows 7 以降、PnP マネージャーを使用して、[コンテナー ID](container-ids.md)デバイスの識別文字列を 1 つまたは複数デバイス (devnode) するノードのコンピューターにインストールされている物理デバイスの各インスタンスの列挙操作をグループ化します。

各列挙子は、そのデバイス Id、ハードウェア Id、および互換性 Id を列挙するデバイスを一意に識別するをカスタマイズします。 また、ハードウェア Id および互換性 Id を識別するために、独自のポリシーでは各列挙子。 ハードウェア ID とシステム バスのほとんどの互換性のある ID 形式の詳細については、[デバイス識別子の形式](device-identifier-formats.md)を参照してください。
