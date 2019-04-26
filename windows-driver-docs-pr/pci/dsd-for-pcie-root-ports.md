---
title: PCIe ルート ポートのデバイス固有データ (_DSD)
description: 最新のスタンバイとホット PCI サポートするための ACPI _DSD メソッド プラグイン シナリオ
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI、ACPI \_DSD メソッド
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9746d3bc2f43bbc6e82e580261b3380386cb956
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352942"
---
# <a name="acpi-interface-device-specific-data-dsd-for-pcie-root-ports"></a>ACPI インターフェイス:PCIe ルート ポートのデバイス固有データ (_DSD)

Windows 10 (バージョン 1803)、最新の Standby および PCI のホット プラグ シナリオをサポートする新しい ACPI _DSD メソッドが追加されました。
## <a name="directed-deepest-runtime-idle-platform-state-drips-support-on-pcie-root-ports"></a>Directed PCIe ルート ポートで最も深いランタイム アイドル プラットフォームの状態 (DRIPS) のサポート 

 この ACPI オブジェクトは、最新のスタンバイ対応デスクトップ システムでユーザーにアクセスできるすべての PCIe ルート ポート/スロットの ACPI スコープ内で実装しなければなりません。 

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

この ACPI オブジェクトにより、オペレーティング システムを特定し、電源 D3 状態のときに、ホット プラグ イベントを処理できる PCIe ルート ポートを管理します。 このオブジェクトが実装されていない場合、PCIe のホット プラグ可能なポートは、その後、システムの電源が入らない子 PCIe デバイス、必要に応じてより多くの電力を消費するシステムを持っていない場合は、このポートを管理します。

Thunderbolt™ 階層、ランタイム D3 上のすべての PCIe ルート ポートでこのオブジェクトを実装する必要があります (RTD3) 対応のシステム、ルート ポート ACPI デバイスのスコープ内で。

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

この ACPI オブジェクトは、外部に公開されている PCIe 階層 (Thunderbolt™ など) を識別するために、オペレーティング システムを使用します。 このオブジェクトは、ルート ポート ACPI デバイスのスコープ内で実装する必要があります。

注:Windows 10 1803 と配布システムでのみ実装 Thunderbolt™ 階層の PCIe ルート ポートでします。

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
## <a name="see-also"></a>関連項目

[PCI を有効にする Windows のネイティブ コントロールを Express](enabling-pci-express-native-control.md)
