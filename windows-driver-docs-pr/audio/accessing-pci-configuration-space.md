---
title: PCI 構成領域へのアクセス
description: PCI 構成領域へのアクセス
ms.assetid: 4ec520db-7976-40e8-8336-f9056dc024b1
keywords:
- PCI 構成領域 WDK オーディオ
- オーディオアダプタードライバー WDK、PCI 構成領域
- アダプタードライバー WDK オーディオ、PCI 構成領域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7225db48bdd93155e777fe927822b314a331ada4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831409"
---
# <a name="accessing-pci-configuration-space"></a>PCI 構成領域へのアクセス


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


Windows Me/98 および Windows 2000 以降では、アダプタードライバーは、IRQL を使用して、IRQL パッシブ\_レベルでアダプターカードの PCI 構成領域にアクセスできます。これを行うには、 [**irp\_\_読み取り\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と irp\_\_書き込み @no を使用し[**構成要求 (_s)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config) 。

Windows 2000 以降では、PCI ドライバースタックによって[**バス\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスがエクスポートされます。これにより、IRQL ディスパッチ\_レベルで pci 構成領域にアクセスできるようになります。

詳細については、「[デバイスの構成領域へのアクセス](https://docs.microsoft.com/windows-hardware/drivers/kernel/accessing-device-configuration-space)」を参照してください。

 

 




