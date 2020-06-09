---
title: デバイス ドライバーのための DMA 再マッピングを有効にする
description: 直接メモリアクセス (DMA) の再マッピングを有効にし、オプトインして、カーネル DMA 保護と DMAGuard との互換性を確保します。
ms.date: 05/16/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3ba29a13a3cc1849512118f2114a5d6f2fca5bc8
ms.sourcegitcommit: 188596c90e03a5619b5cbf0bff4276fc94777253
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84530243"
---
# <a name="enabling-dma-remapping-for-device-drivers"></a>デバイス ドライバーのための DMA 再マッピングを有効にする

[カーネル DMA 保護](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt) と [DMAGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy) との互換性を確保するために、PCIe デバイス ドライバーは直接メモリ アクセス (DMA) の再マッピングをオプトインできます。

デバイス ドライバーの DMA の再マッピングにより、メモリの破損や悪意のある DMA 攻撃から保護され、デバイスの互換性が向上します。 また、DMA 再マッピング互換性のあるドライバーを使用しているデバイスは、ロック画面の状態に関係なく、DMA を開始および実行できます。

カーネル DMA 保護が有効になっているシステムでは、DMAGuard ポリシーは、システム管理者によって設定されたポリシー値に応じて、[外部](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-externally-exposed-pcie-root-ports)/[露出した](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports#identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection) PCIe ポート (例: M.2、Thunderbolt™) に接続されている、DMA 再マッピング互換性のないデバイスをブロックする可能性があります。

## <a name="driver-requirements-for-enabling-and-opting-into-dma-remapping"></a>DMA の再マッピングを有効にし、オプトインするためのドライバーの要件

1. ドライバーは、次のインターフェイスを使用して DMA を実行します。
    * [WDF DMA インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-dma-in-windows-driver-framework)
    * [WDM インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/)
    * [NDIS インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
2. DMA の再マッピングをオプトインするには、次の INF ディレクティブを指定します。

  ```inf
    [MyServiceInstall_AddReg]
    HKR,Parameters,DmaRemappingCompatible,0x00010001,1
    ;1 = opt-in, 2 = opt-in only for external devices
  ```

3. ドライバーのテスト時にドライバーの検証を有効にします。
    * ドライバー検証 (テスト目的) では、外部デバイスをオプトインするための INF ディレクティブの値が 1 になります。
4. VT-d/AMD-Vi が有効な最新の Windows 10 ビルドを使用して、Intel x64 および AMD64 システムのドライバー機能をテストします。

_注: グラフィックス デバイス ドライバーでは、DMA の再マッピングはサポートされていません。_

## <a name="validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance"></a>特定のデバイス ドライバー インスタンスに対して DMA の再マッピングが有効になっていることを検証する

特定のドライバーが DMA の再マッピングをオプトインしたかどうかを確認するには、デバイスの **[詳細]** タブのデバイス マネージャーで、[DMA 再マッピング ポリシー] プロパティに対応する値を確認します。 デバイス マネージャーのポリシーには、次の 3 つの値を指定できます。

* 2 = 現在、特定のデバイス インスタンスに対して DMA の再マッピングが適用されています。
* 1 = デバイス ドライバーが DMA の再マッピングを明示的にオプトアウトしています。
* 0 または DMA の再マッピング ポリシー プロパティが表示されていない = INF ファイルで DMA 再マッピング INF ディレクティブが指定されていません。 このデバイスには DMA の再マッピングは適用されません。

>[!NOTE]
> Windows 10 バージョン1803および1809の場合、デバイスマネージャーのプロパティフィールドには GUID {83da6326-97a6-4088-9453-a1923f573b29} [18] が使用されます。
