---
title: PCIe ルート ポートのデバイス固有データ (_DSD)
description: 最新のスタンバイおよび PCI ホットプラグのシナリオをサポートするための ACPI _DSD 方法
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI、ACPI \_ DSD 方法
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: be8015d4e8d3751cc443fb61bff9cd5db282d90a
ms.sourcegitcommit: 8973457113e00a5f4a0848a1b3165a42b975e81c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83349880"
---
# <a name="acpi-interface-device-specific-data-_dsd-for-pcie-root-ports"></a>ACPI インターフェイス: \_ PCIe ルートポート用のデバイス固有データ (DSD)

Windows 10 (バージョン 1803) では、 \_ 最新のスタンバイおよび PCI ホットプラグのシナリオをサポートするために、新しい ACPI DSD メソッドが追加されています。

## <a name="directed-deepest-runtime-idle-platform-state-drips-support-on-pcie-root-ports"></a>PCIe ルートポートでの、基本的に最も深いランタイムアイドルプラットフォーム状態 (DRIPS) のサポート

 この ACPI オブジェクトは、[有向電源管理フレームワーク (DFx)](../kernel/introduction-to-the-directed-power-management-framework.md)を実装できる最新のスタンバイ対応システムでユーザーがアクセスできるすべての PCIe ルートポート/スロットの acpi スコープに実装する必要があります。

```ASL
Name (_DSD, Package () {

          ToUUID("FDF06FAD-F744-4451-BB64-ECD792215B10"),

            Package () {

                Package (2) {"FundamentalDeviceResetTriggeredOnD3ToD0", 1},
            }
        }
)
```

## <a name="identifying-pcie-root-ports-supporting-hot-plug-in-d3"></a>D3 でのホット プラグをサポートする PCIe ルート ポートの識別

この ACPI オブジェクトにより、オペレーティングシステムは、D3 状態のときにホットプラグイベントを処理できる PCIe ルートポートを特定し、電源管理を行うことができます。 このオブジェクトが PCIe ホットプラグ対応ポートに実装されていない場合、このポートに子 PCIe デバイスがないと、システムはこのポートを電源管理しません。これにより、システムは必要以上に多くの電力を消費します。

このオブジェクトは、ルートポート ACPI デバイススコープの Thunderbolt icon 階層のすべての PCIe ルートポート (実行時 D3 (RTD3) 対応システム上) に実装する必要があります。

```ASL
Name (_DSD, Package () {  

        ToUUID("6211E2C0-58A3-4AF3-90E1-927A4E0C55A4"),  

        Package () {  

            Package (2) {"HotPlugSupportInD3", 1},  

                   }
        }
)
```

## <a name="identifying-externally-exposed-pcie-root-ports"></a>外部に公開されている PCIe ルート ポートの識別

この ACPI オブジェクトを使用すると、オペレーティングシステムは、Thunderbolt icon など、外部から公開されている PCIe 階層を識別できます。 このオブジェクトは、ルートポートの ACPI デバイススコープに実装する必要があります。

注: Windows 10 バージョン1803で出荷されるシステムでは、このオブジェクトは Thunderbolt icon 階層の PCIe ルートポートにのみ実装する必要があります。

```ASL
Name (_DSD, Package () {  

ToUUID("EFCC06CC-73AC-4BC3-BFF0-76143807C389"),
Package () {
Package (2) {"ExternalFacingPort", 1}, // Property 1: This is an externally facing port/hierarchy
Package (2) {"UID", 0}, // Property 2: UID of the externally facing port on platform, range is: 0, 1, …, n-1
                   }
        }
)
```

## <a name="identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection"></a>ユーザーがアクセスできる内部の PCIe ポートを特定し、DMA による保護を必要とする

この ACPI オブジェクトを使用すると、オペレーティングシステムは、ユーザーが簡単にアクセスできる内部の PCIe 階層 (たとえば、ラッチによってアクセスできるラップトップの M. 2 PCIe スロット) を識別し、OS[カーネル DMA 保護](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)メカニズムによる保護を必要とします。 このオブジェクトは、ルートポートの ACPI デバイススコープに実装する必要があります。 

メモ: 
-   この ACPI オブジェクトを使用した PCI ポートの保護は、Windows 10 バージョン1903以降でのみサポートされています。
-   OS で DSD を解析 \_ し、必要な保護を PCI ポートに適用するためには、システム BIOS/UEFI でカーネル DMA 保護を有効にする必要があります。
-   このポートに接続されているデバイスのドライバーは、DMA の再マップをサポートする必要があります。それ以外の場合、Windows 10 は、 [Dmaguard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard)に応じて、ユーザーがログインするか、または無期限に操作するまで、これらのデバイスの動作をブロックします。


```ASL
Name (_DSD, Package () {  

ToUUID("70D24161-6DD5-4C9E-8070-705531292865"),
Package () {
Package (2) {"DmaProperty", 1}, // Property 1: This port needs to be protected by the OS
Package (2) {"UID", 0}, // Property 2: UID of the PCIe port on platform, range is: 0, 1, …, n-1
                   }
        }
)
```

## <a name="see-also"></a>参照

[Windows での PCI Express ネイティブ コントロールの有効化](enabling-pci-express-native-control.md)

[Thunderbolt™ 3 のカーネル DMA 保護](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)
