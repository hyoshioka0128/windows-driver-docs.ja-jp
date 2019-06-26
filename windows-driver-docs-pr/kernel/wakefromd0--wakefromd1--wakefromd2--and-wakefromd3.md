---
title: WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3
description: WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3
ms.assetid: f01aaceb-babf-42da-bc4b-1a846c84a313
keywords:
- WakeFromD0
- WakeFromD1
- WakeFromD2
- WakeFromD3
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b90c70565ee9992607398f8fcc10923ee03fdd96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358117"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3





これらの各[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体のメンバーは、デバイスことができます、デバイスが指定された状態を受信する外部のシグナルへの応答がスリープ解除するかどうかを示します。

すべての 4 つのデバイスの電源をサポートするデバイスのことができます (D0、D1、D2、D3) の状態を再開状態 D0 および D1 からのみ、 **WakeFromD0**と**WakeFromD1**ビットが設定されている、 **WakeFromD2**と**WakeFromD3**のビットがクリアされます。

 

 




