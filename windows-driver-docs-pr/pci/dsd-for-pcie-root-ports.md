---
title: PCIe ルート ポートのデバイス固有データ (_DSD)
description: 最新のスタンバイおよび PCI ホットプラグのシナリオをサポートするための ACPI _DSD 方法
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI、ACPI \_DSD 方法
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 068544e52664ad138bac65aecc508dedbb174b76
ms.sourcegitcommit: 508e275021b34197fedd82b3649c9b59b471300b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82039791"
---
# <a name="acpi-interface-device-specific-data-_dsd-for-pcie-root-ports"></a>ACPI インターフェイス: PCIe ルートポート用のデバイス固有のデータ (_DSD)

Windows 10 (バージョン 1803) では、最新のスタンバイおよび PCI ホットプラグのシナリオをサポートするために、新しい ACPI _DSD メソッドが追加されています。

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

このオブジェクトは、ルートポート ACPI デバイススコープの Thunderbolt icon™階層のすべての PCIe ルートポート、実行時 D3 (RTD3) 対応システム上に実装する必要があります。

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

この ACPI オブジェクトを使用すると、オペレーティングシステムで外部に公開されている PCIe 階層を識別できます (例: Thunderbolt icon™)。 このオブジェクトは、ルートポートの ACPI デバイススコープに実装する必要があります。

注: Windows 10 1803 が出荷されたシステムでは、Thunderbolt icon™階層の PCIe ルートポートにのみ実装する必要があります。

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

## <a name="see-also"></a>参照

[Windows での PCI Express ネイティブ コントロールの有効化](enabling-pci-express-native-control.md)
