---
title: Storport ミニポートドライバーでの DMA の再マップのサポート
description: Storport ミニポートドライバーでの DMA の再マップのサポート
ms.assetid: 9d1e1549-8b11-4a9a-b068-7b1d75c58e52
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: f9940e5086ff147f7a122af9890e40fd83a9f7b9
ms.sourcegitcommit: 3b69a8db54229c2fcf150015c47a89d65dc775ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303359"
---
# <a name="dma-remapping-support-in-storport-miniport-drivers"></a>Storport ミニポートドライバーでの DMA の再マップのサポート

[Storahci storport ミニポートドライバー](https://github.com/microsoft/Windows-driver-samples/tree/master/storage/miniports/storahci)のサンプルコードは、Storport ミニポートドライバーで DMA の再マップをサポートする方法を示しています。 DMA の再マップとカーネル DMA の保護の詳細については、「[デバイスドライバーの dma の](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers)再割り当てを有効にする」を参照してください。

> [!NOTE]
>
> Storport ミニポートドライバーの場合、「[特定のデバイスドライバーインスタンスに対して dma 再マップが有効になっていることを検証する](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers#validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance)」で説明されている "dma 再マップポリシー" のデバイスプロパティの既定値は、windows 10 バージョン1803および1809の場合は0、windows 10 バージョン1903以降の場合は2です。

このプロパティは**DEVPKEY_Device_DmaRemappingPolicy**に対応しています。
