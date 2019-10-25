---
title: アクションインターフェイス
description: アクションインターフェイスは、IWDTFTarget2 インターフェイスのインスタンスを制御します。 各プラグインは、このインターフェイスをサポートする必要があります。
keywords:
- Windows デバイステストフレームワーク WDK、アクションインターフェイス
- WDTF WDK、アクションインターフェイス
- アクションインターフェイス WDK WDTF
- COM インターフェイス WDK WDTF
- インターフェイス WDK WDTF
ms.date: 04/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: a095ec35b2da254ed80a5b4292138bf51710be4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841671"
---
# <a name="action-interfaces"></a>アクションインターフェイス

アクションインターフェイスは、 [IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)インターフェイスのインスタンスを制御します。 各プラグインは、このインターフェイスをサポートする必要があります。 すべてのアクションインターフェイスは、直接または間接的に[iaction](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iaction)から継承します。 

IWDTFTarget2:: GetInterface メソッドを呼び出すことによって、ターゲットのアクションインターフェイスを取得できます。

アクションインターフェイスには、デバイスアクションインターフェイスとシステムアクションインターフェイスの2つのセットがあります。

### <a name="device-action-interfaces"></a>デバイスアクションインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  インポートおよび事前にインポートされたドライバーパッケージのドライバーパッケージを表す操作とプロパティを定義します。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | ドライバーのセットアップ中に対象デバイスを制御する操作を定義します。 |
|[IWDTFEnhancedDeviceTestSupportAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 拡張デバイステスト (EDT) フィルタードライバーをサポートする操作とプロパティを定義します。 |
|[IWDTFEnhancedDeviceTestSupportActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 拡張デバイステスト (EDT) アクションのコレクションをサポートする操作とプロパティを定義します。 |
|[IWDTFPNPAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | プラグアンドプレイ (PNP) デバイス関連のテストインターフェイスの操作とプロパティを定義します。 |
|[IWDTFPNPActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |プラグアンドプレイ (PNP) デバイス関連のテストインターフェイスのコレクションの操作とプロパティを定義します。 |
|[IWDTFSimpleIOEx2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 単純な同期 i/o 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 単純な非同期 i/o 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 単純な非同期 i/o 機能テストのコレクションの操作を定義します。 |
 
### <a name="system-action-interfaces"></a>システムアクションインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | ドライバーのセットアップ中にシステムを制御する操作を定義します。 |
|[IWDTFSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | ドライバーのテストをサポートする操作とプロパティを定義します。 |
 

## <a name="remarks"></a>解説

WDTF では、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インターフェイスは、多数の SimpleIO 実装のラッパーとして1回実装されます。

SimpleIO は、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)を使用するのではなく、直接使用する方が簡単です。 これは、シナリオコードでは、開始する各[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスへの参照を保持する必要があり、終了する前に停止しておく必要があるためです。 ただし、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)は非同期に実行されるため、イベントの組み合わせをテストすることができます。 たとえば、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスは、ハードウェアスリープ機能をテストするために、長時間にわたって i/o テストを開始できます。

## <a name="requirements"></a>前提条件

| ヘッダー|
|-|
|[WDTFDriverPackageAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/index) |
|[WDTFEDTAction. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfedtaction/index) |
|[WDTFPNPAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/index) |


## <a name="see-also"></a>関連項目
[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2:: GetInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 
