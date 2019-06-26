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
ms.openlocfilehash: cc96eac37b3e58b5c56d31177d18a30a003a5a5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355781"
---
# <a name="accessing-pci-configuration-space"></a>PCI 構成領域へのアクセス


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


Windows で Me/98、Windows 2000 以降のアダプター ドライバーが IRQL パッシブに、そのアダプター カードの PCI 構成領域にアクセスできると\_レベルを使用して、 [ **IRP\_MN\_読み取り\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と[ **IRP\_MN\_書き込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)要求。

Windows 2000 以降では、PCI ドライバー スタックのエクスポート、 [ **BUS\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard) IRQL ディスパッチで PCI 構成領域へのアクセスを提供するインターフェイス\_レベル。

詳細については、次を参照してください。[へのアクセスのデバイス構成領域](https://docs.microsoft.com/windows-hardware/drivers/kernel/accessing-device-configuration-space)します。

 

 




