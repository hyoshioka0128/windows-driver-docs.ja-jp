---
title: アクション インターフェイス
description: アクションのインターフェイスは、IWDTFTarget2 インターフェイスのインスタンスを制御します。 各プラグインはこのインターフェイスをサポートする必要があります。
keywords:
- Windows デバイスのテスト フレームワーク WDK、アクションのインターフェイス
- WDTF WDK、アクションのインターフェイス
- アクションは、WDK WDTF をインターフェイスします。
- COM インターフェイスの WDK WDTF
- WDK WDTF インターフェイス
ms.date: 04/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60b71582afea95abed27dd36b46904c8bbd0d52b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347974"
---
# <a name="action-interfaces"></a>アクション インターフェイス

アクションのインターフェイスのインスタンスを制御する、 [IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)インターフェイス。 各プラグインはこのインターフェイスをサポートする必要があります。 アクションのすべてのインターフェイスを継承[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)、直接または間接的にします。 

IWDTFTarget2::GetInterface メソッドを呼び出すことによって、アクションのインターフェイスをターゲットを取得できます。

アクションのインターフェイスの 2 つのセットがあります。 デバイス アクションのインターフェイスとシステム アクション インターフェイス。

### <a name="device-action-interfaces"></a>デバイス アクションのインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  操作とドライバー パッケージをインポートし、インポート済みのドライバー パッケージを表すプロパティを定義します。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | ドライバーのセットアップ中にターゲット デバイスを制御する操作を定義します。 |
|[IWDTFEnhancedDeviceTestSupportAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 操作と、強化されたデバイス テスト (EDT) フィルター ドライバーをサポートするプロパティを定義します。 |
|[IWDTFEnhancedDeviceTestSupportActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 操作および強化されたデバイス テスト (EDT) アクションのコレクションをサポートするプロパティを定義します。 |
|[IWDTFPNPAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | 操作と、プラグ アンド プレイ (PNP) デバイスに関連するテストのインターフェイスのプロパティを定義します。 |
|[IWDTFPNPActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |操作とプラグ アンド プレイ (PNP) デバイスに関連するテスト インターフェイスのコレクションのプロパティを定義します。 |
|[IWDTFSimpleIOEx2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 単純な同期 I/O 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 単純な非同期 I/O 機能テストの操作を定義します。 |
|[IWDTFSimpleIOStressActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 単純な非同期 I/O の機能テストのコレクションの操作を定義します。 |
 
### <a name="system-action-interfaces"></a>システム操作のインターフェイス

| インターフェイス | 説明 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | ドライバーのセットアップ中に、システムを制御する操作を定義します。 |
|[IWDTFSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | 操作とドライバーのテストをサポートするプロパティを定義します。 |
 

## <a name="remarks"></a>注釈

WDTF で、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)多数 SimpleIO 実装のラッパーとしてインターフェイスが 1 回実装します。

を直接使用しやすくなります SimpleIO なくを通じて[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)します。 これは、シナリオのコードは、それぞれへの参照を保持する必要があるため[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスを開始するには、しを閉じる前に停止することに注意してください。 ただし、ため[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 、非同期的に実行されるイベントの組み合わせをテストできます。 たとえば、 [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)インスタンスが I/O がハードウェアのスリープ機能をテストする長期間にわたってテストを開始する可能性があります。

## <a name="requirements"></a>要件

| Header|
|-|
|[WDTFDriverPackageAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/index) |
|[WDTFEDTAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/index) |
|[WDTFPNPAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/index) |


## <a name="see-also"></a>関連項目
[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2::GetInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 
