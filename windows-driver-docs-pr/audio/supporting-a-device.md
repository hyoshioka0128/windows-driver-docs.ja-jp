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
ms.openlocfilehash: dc78c0b0edf81c7983bbf37d02f78ecb87e9b1b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582017"
---
# <a name="supporting-a-device"></a>デバイスのサポート


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls システム ドライバー (*Portcls.sys*) をレンダリングし、wave と MIDI ストリームをキャプチャするオーディオ デバイスをサポートするいくつかの組み込みのポート ドライバーを提供します。

基底インターフェイスから派生するインターフェイスを公開するポートのすべてのドライバー [IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)します。 **IPort**基底インターフェイスからメソッドを継承**IUnknown**します。 **IPort**次の追加のメソッドを提供します。

[**IPort::GetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff536941)

レジストリからオーディオのアダプターのプラグ アンド プレイ プロパティを取得します。
[**IPort::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536943)

ポート オブジェクトを初期化します。
[**IPort::NewRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff536945)

新しいレジストリ キーを作成するか、既存のキーを開きます。
PortCls には、次のポートのドライバーが実装されています。

[WaveCyclic ポート ドライバー](wavecyclic-port-driver.md)

[WavePci ポート ドライバー](wavepci-port-driver.md)

[WaveRT ポート ドライバー](wavert-port-driver.md)

[トポロジ ポート ドライバー](topology-port-driver.md)

[MIDI ポート ドライバー](midi-port-driver.md)

[Dmu ポート ドライバー](dmus-port-driver.md)

 

 




