---
title: デバイスのサポート
description: デバイスのサポート
ms.assetid: 5f60d3aa-6061-40f7-8108-d752534b88ed
keywords:
- オーディオのミニポート ドライバー WDK、デバイスのサポート
- ミニポート ドライバー WDK、オーディオ デバイス サポート
- ポート クラス ドライバー WDK オーディオ
- PortCls WDK、オーディオ デバイスのサポート
- ポート ドライバー WDK オーディオ、ミニポート ドライバー
- ポート ドライバー WDK オーディオ、ポート クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1410d6abc90842112044136429ae642ed6462a74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354221"
---
# <a name="supporting-a-device"></a>デバイスのサポート


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls システム ドライバー (*Portcls.sys*) をレンダリングし、wave と MIDI ストリームをキャプチャするオーディオ デバイスをサポートするいくつかの組み込みのポート ドライバーを提供します。

基底インターフェイスから派生するインターフェイスを公開するポートのすべてのドライバー [IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)します。 **IPort**基底インターフェイスからメソッドを継承**IUnknown**します。 **IPort**次の追加のメソッドを提供します。

[**IPort::GetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-getdeviceproperty)

レジストリからオーディオのアダプターのプラグ アンド プレイ プロパティを取得します。
[**IPort::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-init)

ポート オブジェクトを初期化します。
[**IPort::NewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-newregistrykey)

新しいレジストリ キーを作成するか、既存のキーを開きます。
PortCls には、次のポートのドライバーが実装されています。

[WaveCyclic ポート ドライバー](wavecyclic-port-driver.md)

[WavePci ポート ドライバー](wavepci-port-driver.md)

[WaveRT ポート ドライバー](wavert-port-driver.md)

[トポロジ ポート ドライバー](topology-port-driver.md)

[MIDI ポート ドライバー](midi-port-driver.md)

[Dmu ポート ドライバー](dmus-port-driver.md)

 

 




