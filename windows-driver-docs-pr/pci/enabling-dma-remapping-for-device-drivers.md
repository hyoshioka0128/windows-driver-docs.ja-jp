---
title: デバイスドライバーの DMA 再マップの有効化
description: 直接メモリアクセス (DMA) の再マッピングを有効にし、オプトインして、カーネル DMA 保護と DMAGuard との互換性を確保します。
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7c53e633b4e56528a088bafad1b65037f056cf32
ms.sourcegitcommit: 3b69a8db54229c2fcf150015c47a89d65dc775ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301474"
---
# <a name="enabling-dma-remapping-for-device-drivers"></a>デバイスドライバーの DMA 再マップの有効化

[カーネル DMA 保護](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt) と [DMAGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy) との互換性を確保するために、PCIe デバイス ドライバーは直接メモリ アクセス (DMA) の再マッピングをオプトインできます。

デバイスドライバーの DMA の再マップにより、メモリの破損や悪意のある DMA 攻撃から保護され、デバイスの互換性が向上します。 また、DMA の再マップと互換性のあるドライバーを持つデバイスは、ロック画面の状態に関係なく、DMA を開始および実行できます。

カーネル DMA 保護が有効になっているシステムでは、 [external](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-externally-exposed-pcie-root-ports) / システム管理者によって設定されたポリシー値に応じて、外部に[公開](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection)されている PCIe ポート (例: M. 2, thunderbolt icon™) に接続されている dma 再マップと互換性のないドライバーを使用してデバイスをブロックすることができます。

## <a name="driver-requirements-for-enabling-and-opting-into-dma-remapping"></a>DMA の再マップを有効にし、オプトインするためのドライバーの要件

ドライバーは、次のインターフェイスを使用して DMA を実行します。

* [WDF DMA インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-dma-in-windows-driver-framework)
* [WDM インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/)
* [NDIS インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

ドライバーの DMA 再マップポリシーを調整するには、次のような INF ディレクティブをサービスインストールセクションに追加します。

  ```inf
    [MyServiceInstall_AddReg]
    HKR,Parameters,DmaRemappingCompatible,0x00010001,1    ; where 1 = opt-in
  ```
  
**DmaRemappingCompatible**の有効な値は次のとおりです。

| 値 | 意味 |
| ----- | ------- |
| 0     | オプトアウト。これは、ドライバーが DMA 再マップと互換性がないことをシステムに示します。 |
| 1     | 利用することを選択します。 これは、ドライバーが DMA の再マップと完全に互換性があることをシステムに示しています。 |
| 2     | オプトインします。ただし、次の条件のうち1つ以上が満たされている場合にのみ選択します。デバイスが外部デバイスの場合 (例: Thunderbolt icon);B. ドライバー検証ツールで DMA 検証が有効になっている場合。 |
| レジストリキーがありません | システムでポリシーを決定します。 |

ドライバーをテストするときに、ドライバーの検証ツールを有効にします。 ドライバー検証ツールでテストを行う場合、外部デバイスをオプトインするための INF ディレクティブの値は1に昇格されます。

VT-d/AMD-Vi が有効な最新の Windows 10 ビルドを使用して、Intel x64 および AMD64 システムのドライバー機能をテストします。

> [!NOTE]
> グラフィックスデバイスドライバーでは、DMA の再マップはサポートされていません。

## <a name="validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance"></a>特定のデバイスドライバーインスタンスに対して DMA の再マップが有効になっていることを検証しています

特定のドライバーが DMA の再マップを選択したかどうかを確認するには、デバイスの [**詳細**] タブで、[dma 再マップポリシー] プロパティに対応する値についてデバイスマネージャーを確認します。 表示されるプロパティは、 **DEVPKEY_Device_DmaRemappingPolicy**に対応します。 このプロパティの値は、アクティブな DMA 再マップポリシーを示し、次のいずれかの値を指定できます。

| 値 | 意味 |
| ----- | ------- |
| 2     | 現在、特定のデバイスインスタンスに対して DMA の再マップが適用されています。 |
| 1     | デバイスドライバーが DMA の再マップを明示的にオプトアウトした。 |
| 0または DMA の再マップポリシープロパティは表示されません | DMA 再マップ INF ディレクティブが INF ファイルで指定されていません。 このデバイスには DMA の再マップは適用されません。 |

![デバイス マネージャーの [詳細] タブ](images/device-details-tab-1903.png)

>[!NOTE]
> Windows 10 バージョン1803および1809の場合、デバイスマネージャーのプロパティフィールドには GUID {83da6326-97a6-4088-9453-a1923f573b29} [18] が使用されます。
