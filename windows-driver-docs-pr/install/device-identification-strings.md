---
title: デバイス識別文字列
description: プラグアンドプレイ (PnP) マネージャーおよびその他のデバイスインストールコンポーネントは、デバイス識別文字列を使用して、コンピューターにインストールされているデバイスを識別します。
ms.assetid: dae23185-63d9-4a0f-9786-c7fa66368826
keywords:
- 互換性 Id WDK デバイスのインストール
- デバイス Id WDK デバイスのインストール
- デバイスインスタンス Id WDK デバイスのインストール
- ドライバーノードの WDK デバイスのインストール
- ハードウェア Id WDK デバイスのインストール
- インスタンス Id WDK デバイスのインストール
- デバイスのセットアップ WDK デバイスのインストール、デバイス識別文字列
- デバイスのインストール WDK、デバイス識別文字列
- デバイスをインストールする WDK、デバイス id 文字列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb0497c75e24a6bc4738d7aac84f8718bf3f43f
ms.sourcegitcommit: 36b7db40d5a91d8726feb2e2d9d4ece1fb484051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591018"
---
# <a name="device-identification-strings"></a>デバイスの識別用文字列

プラグアンドプレイ (PnP) マネージャーおよびその他の[デバイスインストールコンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)は、デバイス識別文字列を使用して、コンピューターにインストールされているデバイスを識別します。

Windows では、次のデバイス識別文字列を使用して、デバイスに最も一致する情報 (INF) ファイルを検索します。 これらの文字列はデバイスの列挙子によって報告されます。これは、PnP ハードウェア標準に基づいて PnP デバイスを検出するシステムコンポーネントです。 これらのタスクは、pnp マネージャーとのパートナーシップで PnP バスドライバーによって実行されます。 通常、デバイスは、PCI や PCMCIA バスドライバーなどの親バスドライバーによって列挙されます。 一部のデバイスは、ACPI ドライバーなどのバスフィルタードライバーによって列挙されます。

- [ハードウェア Id](hardware-ids.md)

- [互換性 Id](compatible-ids.md)

Windows は、ハードウェア Id または互換性 Id のいずれかに一致するものを見つけようとします。 Windows でこれらの Id を使用してデバイスを INF ファイルと照合する方法、および INF ファイルで Id を指定する方法の詳細については、「 [windows がドライバーを選択する方法](how-setup-selects-drivers.md)」を参照してください。

PnP マネージャーは、上記の Id を使用してデバイスを識別するだけでなく、コンピューターにインストールされている各デバイスのインスタンスを一意に識別するために、次の Id を使用します。

- [インスタンス Id](instance-ids.md)

- [デバイスインスタンス Id](device-instance-ids.md)

Windows 7 以降では、PnP マネージャーは[コンテナー ID](container-ids.md)デバイス識別文字列を使用して、コンピューターにインストールされている物理デバイスの各インスタンスから列挙された1つまたは複数のデバイスノード (devnodes) をグループ化します。

各列挙子は、そのデバイス Id、ハードウェア Id、互換性 Id をカスタマイズして、列挙されるデバイスを一意に識別します。 また、各列挙子には、ハードウェア Id と互換性 Id を識別するための独自のポリシーがあります。 ほとんどのシステムバスのハードウェア ID と互換性のある ID 形式の詳細については、「[デバイス識別子の形式](device-identifier-formats.md)」を参照してください。

> [!NOTE]
> デバイス id 文字列を解析することはできません。 これらは文字列比較のみを目的としており、不透明な文字列として扱う必要があります。

