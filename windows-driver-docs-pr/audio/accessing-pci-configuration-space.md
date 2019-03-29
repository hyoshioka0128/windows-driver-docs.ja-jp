---
title: PCI 構成領域へのアクセス
description: PCI 構成領域へのアクセス
ms.assetid: 4ec520db-7976-40e8-8336-f9056dc024b1
keywords:
- PCI 構成領域 WDK オーディオ
- アダプターのオーディオ ドライバー WDK、PCI 構成領域
- アダプターのドライバー WDK オーディオ、PCI 構成領域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b1ba8f3e1412004c97a482f65706019ad7ec9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571783"
---
# <a name="accessing-pci-configuration-space"></a>PCI 構成領域へのアクセス


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


Windows で Me/98、Windows 2000 以降のアダプター ドライバーが IRQL パッシブに、そのアダプター カードの PCI 構成領域にアクセスできると\_レベルを使用して、 [ **IRP\_MN\_読み取り\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)と[ **IRP\_MN\_書き込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551769)要求。

Windows 2000 以降では、PCI ドライバー スタックのエクスポート、 [ **BUS\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707) IRQL ディスパッチで PCI 構成領域へのアクセスを提供するインターフェイス\_レベル。

詳細については、次を参照してください。[へのアクセスのデバイス構成領域](https://msdn.microsoft.com/library/windows/hardware/ff540450)します。

 

 




