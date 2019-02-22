---
Description: Initializing the Driver
title: ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6145c0b10ae249d1335753ddcdf1f7b86593d14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528276"
---
# <a name="initializing-the-driver"></a>ドライバーの初期化


初期化関数では、 **WpdBaseDriver::Initialize**と**WpdBaseDriver::Uninitialize** WpdHelloWorldDriver サンプルでは空です。 **初期化**関数が単に返される S\_[ok]、**非**関数は何も行いません。

次のサンプル ドライバーからの抜粋のコードを含む**WpdBaseDriver::Initialize**と**WpdBaseDriver::Uninitialize**します。

```ManagedCPlusPlus
/**
 * This method is called to initialize the driver object.
 * This is where the driver would set up its I/O libraries
 * and so on.
 */
HRESULT WpdBaseDriver::Initialize()
{

    return S_OK;
}

/**
 * This method is called to uninitialize the driver object.
 * In a real driver, this is where the driver would clean up
 * any resources held by this driver.
 */
VOID WpdBaseDriver::Uninitialize()
{
}
```

実際のデバイスをサポートするには、このサンプルを移植する場合に-Bluetooth 対応は携帯電話など-で機能を追加すると、**初期化**ドライバーの I/O ライブラリを初期化する関数。 これは、デバイス コマンドを発行します。 このライブラリは、携帯電話の場合、電話帳を列挙するために、または、電話のストレージでファイルを取得または設定するためのコマンドを含めることができます。 最低限、**初期化**関数は、デバイスのネットワーク アドレスを確立します。 **WPDBaseDriver::Uninitialize**関数は、必要なクリーンアップを実行します。

 

 




