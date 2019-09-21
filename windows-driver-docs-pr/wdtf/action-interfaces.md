---
title: アクション インターフェイス
description: アクションインターフェイスは、IWDTFTarget2 インターフェイスのインスタンスを制御します。 各プラグインは、このインターフェイスをサポートする必要があります。
keywords:
- Windows デバイステストフレームワーク WDK、アクションインターフェイス
- WDTF WDK、アクションインターフェイス
- アクションインターフェイス WDK WDTF
- COM インターフェイス WDK WDTF
- インターフェイス WDK WDTF
ms.date: 04/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e6140943bbe05deb2ed59404bb50657af755976
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164795"
---
# <a name="action-interfaces"></a>アクション インターフェイス

アクションインターフェイスは、 [IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)インターフェイスのインスタンスを制御します。 各プラグインは、このインターフェイスをサポートする必要があります。 すべてのアクションインターフェイスは、直接または間接的に[iaction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)から継承します。 

IWDTFTarget2:: GetInterface メソッドを呼び出すことによって、ターゲットのアクションインターフェイスを取得できます。

アクションインターフェイスには、デバイスアクションインターフェイスとシステムアクションインターフェイスの2つのセットがあります。

### <a name="device-action-interfaces"></a>デバイスアクションインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  インポートおよび事前にインポートされたドライバーパッケージのドライバーパッケージを表す操作とプロパティを定義します。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | ドライバーのセットアップ中に対象デバイスを制御する操作を定義します。 |
|[IWDTFEnhancedDeviceTestSupportAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 拡張デバイステスト (EDT) フィルタードライバーをサポートする操作とプロパティを定義します。 |
|[IWDTFEnhancedDeviceTestSupportActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 拡張デバイステスト (EDT) アクションのコレクションをサポートする操作とプロパティを定義します。 |
|[IWDTFPNPAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | プラグアンドプレイ (PNP) デバイス関連のテストインターフェイスの操作とプロパティを定義します。 |
|[IWDTFPNPActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |プラグアンドプレイ (PNP) デバイス関連のテストインターフェイスのコレクションの操作とプロパティを定義します。 |
|[IWDTFSimpleIOEx2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 単純な同期 i/o 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 単純な非同期 i/o 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 単純な非同期 i/o 機能テストのコレクションの操作を定義します。 |
 
### <a name="system-action-interfaces"></a>システムアクションインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | ドライバーのセットアップ中にシステムを制御する操作を定義します。 |
|[IWDTFSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | ドライバーのテストをサポートする操作とプロパティを定義します。 |
 

## <a name="remarks"></a>コメント

WDTF では、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インターフェイスは、多数の SimpleIO 実装のラッパーとして1回実装されます。

SimpleIO は、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)を使用するのではなく、直接使用する方が簡単です。 これは、シナリオコードでは、開始する各[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスへの参照を保持する必要があり、終了する前に停止しておく必要があるためです。 ただし、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)は非同期に実行されるため、イベントの組み合わせをテストすることができます。 たとえば、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスは、ハードウェアスリープ機能をテストするために、長時間にわたって i/o テストを開始できます。

## <a name="requirements"></a>要件

| Header|
|-|
|[WDTFDriverPackageAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/index) |
|[WDTFEDTAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/index) |
|[WDTFPNPAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/index) |


## <a name="see-also"></a>関連項目
[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2:: GetInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 
