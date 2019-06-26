---
title: WDM デバイス オブジェクトの種類
description: WDM デバイス オブジェクトの種類
ms.assetid: 89cc888d-3097-4637-96d2-6b9c59878d2f
keywords:
- 機能のデバイス オブジェクトの WDK カーネル
- FDO WDK カーネル
- 物理デバイス オブジェクトの WDK カーネル
- Pdo WDK カーネル
- デバイス オブジェクト WDK カーネルの種類
- フィルター DOs WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1f8bc429fc7b3b48594dd161e4fc5648216ab6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382945"
---
# <a name="types-of-wdm-device-objects"></a>WDM デバイス オブジェクトの種類





WDM デバイス オブジェクトの 3 つの種類があります。

1.  物理デバイス オブジェクト (PDO) – にバス上のデバイスを表す、[バス ドライバー](bus-drivers.md)します。

2.  機能のデバイス オブジェクト (FDO) – にデバイスを表す、[関数ドライバー](function-drivers.md)します。

3.  デバイス オブジェクトのフィルター (フィルター操作を行います) – デバイスを表します、[フィルター ドライバー](filter-drivers.md)します。

次の 3 つの種類のデバイス オブジェクトは、型のすべて[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)が、異なる方法で使用され、別のデバイスの拡張機能を持つことができます。

ドライバーは、デバイス オブジェクトを作成してデバイスの I/O を処理するドライバーのスタックに追加します ([**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)) と、デバイス スタックへの追加 ([ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack))。 **IoAttachDeviceToDeviceStack**デバイス スタックの現在の先頭を決定し、デバイス スタックの一番上に新しいデバイス オブジェクトをアタッチします。

 

 




