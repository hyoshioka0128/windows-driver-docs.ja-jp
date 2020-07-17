---
title: Storport ミニポート ドライバーでの DMA 再マッピングのサポート
description: Storport ミニポート ドライバーでの DMA 再マッピングのサポート
ms.assetid: 9d1e1549-8b11-4a9a-b068-7b1d75c58e52
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e28d0708fd2927bd26f050a03a2a6b392aee3c1
ms.sourcegitcommit: 1ab8fc6d15fac78ce243f3852d86733ebfca40dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86436880"
---
# <a name="dma-remapping-support-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーでの DMA 再マッピングのサポート

[Storahci storport ミニポートドライバー](https://github.com/microsoft/Windows-driver-samples/tree/master/storage/miniports/storahci)のサンプルコードは、Storport ミニポートドライバーで DMA の再マップをサポートする方法を示しています。 DMA の再マップとカーネル DMA の保護の詳細については、「[デバイスドライバーの dma の](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers)再割り当てを有効にする」を参照してください。

> [!NOTE]
>
> Storport ミニポートドライバーの場合、「[特定のデバイスドライバーインスタンスに対して dma 再マップが有効になっていることを検証する](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers#validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance)」で説明されている "dma 再マップポリシー" のデバイスプロパティの既定値は、windows 10 バージョン1803および1809の場合は0、windows 10 バージョン1903以降の場合は2です。

このプロパティは[**DEVPKEY_Device_DmaRemappingPolicy**](../install/devpkey-device-dmaremappingpolicy.md)に対応しています。
