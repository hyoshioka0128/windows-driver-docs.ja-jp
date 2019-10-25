---
title: DeviceD1 と DeviceD2
description: DeviceD1 と DeviceD2
ms.assetid: 88e9e1bf-c797-4e00-b540-1b2f8d48300a
keywords:
- DeviceD1
- DeviceD2
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d583fa7d4aab57f7c58a13dc64cffad5c98e32d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838741"
---
# <a name="deviced1-and-deviced2"></a>DeviceD1 と DeviceD2





[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の**DeviceD1**メンバーと**DeviceD2**メンバーは、デバイスのハードウェアがこれらのデバイスの電源状態をサポートしているかどうかを示します。 各は1つのビットで、デバイスが状態をサポートする場合に設定され、デバイスが状態をサポートしていない場合はクリアされます。 オペレーティングシステムでは、すべてのデバイスが D0 および D3[デバイスの電源状態](device-power-states.md)をサポートしていることを前提としています。

 

 




