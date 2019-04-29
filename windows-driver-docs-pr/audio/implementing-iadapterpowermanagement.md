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
ms.openlocfilehash: 0842559071363d3b53072d8b6326082b65d4a32f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333634"
---
# <a name="implementing-iadapterpowermanagement"></a>IAdapterPowerManagement の実装


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


実装する場合、 [IAdapterPowerManagement](https://msdn.microsoft.com/library/windows/hardware/ff536485) 、ドライバーのためのインターフェイスの実装を参照してください、 **CAdapterCommon**サンプル オーディオ ドライバーには、Microsoft Windows Driver Kit (クラスWDK)。 このクラスは、デバイスの割り込みを処理し、他のすべてのアダプターのオーディオ ドライバーに共通する機能を実行します。 アダプターの**CAdapterCommon**クラスから継承する必要があります、 **IAdapterPowerManagement**インターフェイスし、では、このインターフェイスをサポートしてその**NonDelegatingQueryInterface**メソッド。 (詳細については、呼び出しのインターフェイスは、の説明を参照してください、 **INonDelegatingUnknown**インターフェイスです。)。

実装を使用する\_ヘッダー ファイルの関数宣言を追加する Portcls.h から IAdapterPowerManagement 定義、 [ **IAdapterPowerManagement::PowerChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff536488)、 [**IAdapterPowerManagement::QueryPowerChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff536490)、および[ **IAdapterPowerManagement::QueryDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff536489)メソッドドライバーの**CAdapterCommon**クラスの定義。

PortCls システム ドライバーのアダプターのデバイスのスタートアップ ルーチンの呼び出し中に (を参照してください[デバイスを起動](https://msdn.microsoft.com/library/windows/hardware/ff563849))、アダプターを登録する必要があります、 **IAdapterPowerManagement**インターフェイス PortCls を呼び出すことによって[ **PcRegisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537724)します。 コード例では、次を参照してください。、 **StartDevice** WDK で Sb16 サンプル アダプターのドライバーでの関数。 **PcRegisterAdapterPowerManagement**関数の最初のパラメーターは、 **IUnknown**アダプター ドライバーへのポインター **CAdapterCommon**オブジェクト。 PortCls クエリに対して、このオブジェクトの**IAdapterPowerManagement**インターフェイス。

PortCls がアダプター ドライバーを呼び出すときに**IAdapterPowerManagement::PowerChangeState**メソッドを変更するデバイスの電源状態では、アダプターのドライバーはアダプターの 新しい電源の状態をデバイスをキャッシュする必要があります**CAdapterCommon**オブジェクト。 中に、 **CAdapterCommon::Init** (WDK のサンプル アダプターのドライバーでの実装を参照してください) を呼び出し、ドライバーは PowerDeviceD0 に初期の電源の状態を設定する必要があります (で説明されている[DeviceState](https://msdn.microsoft.com/library/windows/hardware/ff543087)) する前に正常に初期化から取得します。 ドライバーは、適切な電源状態であることがわかっている場合にのみ、ハードウェアに書き込む必要があります。 WDK で Sb16 サンプル ドライバー、たとえば、ドライバー書き込みを行います PowerDeviceD0 状態でのみハードウェア。

応答を切る前に、 **PowerChangeState**呼び出し、アダプター ドライバーがオーディオ出力、状態にスピーカー ノイズが電源オフにする際に発生するを防止します。 たとえば、シャット ダウン プロセスには、ランプ、DAC が 0 の場合、Dac を無効にし、MIDI 行をミュートに出力が含まれます。

 

 




