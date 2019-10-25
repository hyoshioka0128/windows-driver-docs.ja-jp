---
title: デバイスのサポート
description: デバイスのサポート
ms.assetid: 5f60d3aa-6061-40f7-8108-d752534b88ed
keywords:
- オーディオミニポートドライバー WDK、デバイスサポート
- ミニポートドライバー WDK オーディオ、デバイスサポート
- ポートクラスドライバー WDK オーディオ
- PortCls WDK audio, デバイスサポート
- ポートドライバー WDK オーディオ、ミニポートドライバー
- ポートドライバー WDK オーディオ、ポートクラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 250cb36a47e969d718b02601d1090f8dc1a52e6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830098"
---
# <a name="supporting-a-device"></a>デバイスのサポート


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls システムドライバー (*PortCls*) には、WAVE および MIDI ストリームをレンダリングしてキャプチャするオーディオデバイスをサポートするための組み込みのポートドライバーがいくつか用意されています。

すべてのポートドライバーは、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)から派生したインターフェイスを公開します。 **IPort**は、基本インターフェイス**IUnknown**からメソッドを継承します。 **IPort**には、次の追加のメソッドが用意されています。

[**IPort:: GetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-getdeviceproperty)

オーディオアダプターのプラグアンドプレイプロパティをレジストリから取得します。
[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)

ポートオブジェクトを初期化します。
[**IPort:: NewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-newregistrykey)

新しいレジストリキーを作成するか、既存のキーを開きます。
PortCls は、次のポートドライバーを実装しています。

[WaveCyclic ポートドライバー](wavecyclic-port-driver.md)

[WavePci ポートドライバー](wavepci-port-driver.md)

[WaveRT ポートドライバー](wavert-port-driver.md)

[トポロジポートドライバー](topology-port-driver.md)

[MIDI ポートドライバー](midi-port-driver.md)

[DMus ポートドライバー](dmus-port-driver.md)

 

 




