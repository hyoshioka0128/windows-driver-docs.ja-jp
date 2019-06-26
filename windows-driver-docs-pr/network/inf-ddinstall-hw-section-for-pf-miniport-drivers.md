---
title: PF ミニポート ドライバーの INF DDInstall.HW セクション
description: PF ミニポート ドライバーの INF DDInstall.HW セクション
ms.assetid: 65399462-4AF1-401C-87CB-BF387CA0B053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b29a7c827b68e0bc6726d6a94693e682c2ab951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380898"
---
# <a name="inf-ddinstallhw-section-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの INF DDInstall.HW セクション


INF <em>DDInstall</em>**します。HW**のセクションでは通常、レジストリで、デバイスに固有の情報を設定するかどうかと共に使用明示的な**AddReg**ディレクティブまたは**Include**と**必要がある**エントリ。

PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーの INF ファイルが必要、 <em>DDInstall</em>**します。HW** INF の次のエントリを含むセクション。

-   **Include**エントリ、Windows オペレーティング システムに含まれている pci.inf ファイルを指定します。

-   A**必要がある**エントリを指定する、 **PciSriovSupported.HW** pci.inf ファイルから含めるセクション。 このセクションでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするネットワーク アダプターのすべての PF ミニポート ドライバーに適用される標準の INF 設定を定義します。

例を次に、 <em>DDInstall</em>**します。HW** PF ミニポート ドライバーのセクション。

``` syntax
[Device_Inst.NT.HW]

Include=pci.inf
Needs=PciSriovSupported.HW
```

詳細については、 *DDInstall*セクションを参照してください[ネットワーク INF ファイルで DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

詳細については、 *DDInstall*します。ハードウェアのセクションを参照してください[ **INF DDInstall.HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)します。

 

 





