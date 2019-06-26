---
title: IAdapterPowerManagement の実装
description: IAdapterPowerManagement の実装
ms.assetid: 654b86a7-845c-415b-99e4-c7be92cb9b9c
keywords:
- IAdapterPowerManagement
- アダプターのドライバー WDK オーディオ、電源管理
- アダプターのオーディオ ドライバー WDK、電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d652921a7c5d8591c8e90bdf2d806735a61eb4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359913"
---
# <a name="implementing-iadapterpowermanagement"></a>IAdapterPowerManagement の実装


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


実装する場合、 [IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement) 、ドライバーのためのインターフェイスの実装を参照してください、 **CAdapterCommon**サンプル オーディオ ドライバーには、Microsoft Windows Driver Kit (クラスWDK)。 このクラスは、デバイスの割り込みを処理し、他のすべてのアダプターのオーディオ ドライバーに共通する機能を実行します。 アダプターの**CAdapterCommon**クラスから継承する必要があります、 **IAdapterPowerManagement**インターフェイスし、では、このインターフェイスをサポートしてその**NonDelegatingQueryInterface**メソッド。 (詳細については、呼び出しのインターフェイスは、の説明を参照してください、 **INonDelegatingUnknown**インターフェイスです。)。

実装を使用する\_ヘッダー ファイルの関数宣言を追加する Portcls.h から IAdapterPowerManagement 定義、 [ **IAdapterPowerManagement::PowerChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iadapterpowermanagement-powerchangestate)、 [**IAdapterPowerManagement::QueryPowerChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iadapterpowermanagement-querypowerchangestate)、および[ **IAdapterPowerManagement::QueryDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iadapterpowermanagement-querydevicecapabilities)メソッドドライバーの**CAdapterCommon**クラスの定義。

PortCls システム ドライバーのアダプターのデバイスのスタートアップ ルーチンの呼び出し中に (を参照してください[デバイスを起動](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device))、アダプターを登録する必要があります、 **IAdapterPowerManagement**インターフェイス PortCls を呼び出すことによって[ **PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)します。 コード例では、次を参照してください。、 **StartDevice** WDK で Sb16 サンプル アダプターのドライバーでの関数。 **PcRegisterAdapterPowerManagement**関数の最初のパラメーターは、 **IUnknown**アダプター ドライバーへのポインター **CAdapterCommon**オブジェクト。 PortCls クエリに対して、このオブジェクトの**IAdapterPowerManagement**インターフェイス。

PortCls がアダプター ドライバーを呼び出すときに**IAdapterPowerManagement::PowerChangeState**メソッドを変更するデバイスの電源状態では、アダプターのドライバーはアダプターの 新しい電源の状態をデバイスをキャッシュする必要があります**CAdapterCommon**オブジェクト。 中に、 **CAdapterCommon::Init** (WDK のサンプル アダプターのドライバーでの実装を参照してください) を呼び出し、ドライバーは PowerDeviceD0 に初期の電源の状態を設定する必要があります (で説明されている[DeviceState](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)) する前に正常に初期化から取得します。 ドライバーは、適切な電源状態であることがわかっている場合にのみ、ハードウェアに書き込む必要があります。 WDK で Sb16 サンプル ドライバー、たとえば、ドライバー書き込みを行います PowerDeviceD0 状態でのみハードウェア。

応答を切る前に、 **PowerChangeState**呼び出し、アダプター ドライバーがオーディオ出力、状態にスピーカー ノイズが電源オフにする際に発生するを防止します。 たとえば、シャット ダウン プロセスには、ランプ、DAC が 0 の場合、Dac を無効にし、MIDI 行をミュートに出力が含まれます。

 

 




