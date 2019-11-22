---
title: IAdapterPowerManagement の実装
description: IAdapterPowerManagement の実装
ms.assetid: 654b86a7-845c-415b-99e4-c7be92cb9b9c
keywords:
- IAdapterPowerManagement
- アダプタドライバ WDK audio、電源管理
- オーディオアダプタードライバー WDK、電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31ed7462867aff11015e49b61ad34c25b35d7c63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833238"
---
# <a name="implementing-iadapterpowermanagement"></a>IAdapterPowerManagement の実装


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


ドライバーの[Iadapterpowermanagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)インターフェイスを実装する場合は、Microsoft Windows driver KIT (WDK) のサンプルオーディオドライバーの**cadaptercommon**クラスの実装を参照してください。 このクラスは、デバイス割り込みを処理し、すべてのオーディオアダプタードライバーに共通するその他の機能を実行します。 アダプターの**Cadaptercommon**クラスは**Iadapterpowermanagement**インターフェイスから継承し、 **NonDelegatingQueryInterface**メソッドでこのインターフェイスをサポートする必要があります。 (非デリゲートインターフェイスの詳細については、 **INonDelegatingUnknown**インターフェイスの説明を参照してください)。

ヘッダーファイル Portcls の IMP\_IAdapterPowerManagement 定義を使用すると、 [**Iadapterpowermanagement::P owerchangestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-powerchangestate)、 [**Iadapterpowermanagement:: QueryPowerChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querypowerchangestate)の関数宣言を追加できます。[**Iadapterpowermanagement:: QueryDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querydevicecapabilities)メソッドをドライバーの**cadaptercommon**クラス定義にします。

PortCls システムドライバーがアダプターのデバイススタートアップルーチン (「[デバイスの起動](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)」を参照) の呼び出し中に、アダプターは**iadapterpowermanagement**インターフェイスを PortCls に登録する必要が[**あります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement) コード例については、「Sb16 sample adapter driver in the WDK」の「 **Startdevice**関数」を参照してください。 **Pcregisteradapterpowermanagement**関数の最初のパラメーターは、アダプタードライバーの**cadaptercommon**オブジェクトへの**IUnknown**ポインターです。 PortCls は、このオブジェクトの**Iadapterpowermanagement**インターフェイスを照会します。

PortCls がアダプタードライバーの**Iadapterpowermanagement::P owerchangestate**メソッドを呼び出してデバイスの電源状態を変更すると、アダプタードライバーは、アダプターの**cadaptercommon**オブジェクトにデバイスの新しい電源状態をキャッシュする必要があります。 **Cadaptercommon:: Init**呼び出し中 (WDK のサンプルアダプタードライバーの実装を参照してください)、ドライバーは初期の電源状態を PowerDeviceD0 ( [devicestate](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)で説明) に設定してから、初期化が成功したことを返します. ドライバーは、適切な電源状態にあることがわかっている場合にのみ、ハードウェアに書き込む必要があります。 たとえば、WDK の Sb16 サンプルドライバーでは、ドライバーは PowerDeviceD0 状態のハードウェアにのみ書き込みます。

**PowerChangeState**の呼び出しに応答して電源を切る前に、電源スイッチをオフにしたときにスピーカーノイズが発生しないように、アダプタードライバーによってオーディオ出力が状態になります。 たとえば、シャットダウンプロセスには、DAC が0に出力され、Dac がオフになり、MIDI 回線がミュートされていることがあります。

 

 




