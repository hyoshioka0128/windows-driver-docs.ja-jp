---
title: ターゲットの制御
description: ターゲットの制御
ms.assetid: b329e9a2-7d24-4612-9aa1-9d7955a61473
keywords:
- Windows デバイステストフレームワーク WDK、アクションインターフェイス
- WDTF WDK、アクションインターフェイス
- Windows デバイステストフレームワーク WDK、管理可能なテスト
- WDTF WDK、管理可能なテスト
- 管理可能なテスト WDK WDTF
- アクションインターフェイス WDK WDTF
- COM インターフェイス WDK WDTF
- インターフェイス WDK WDTF
- コードモジュール WDK WDTF
- スクリプト WDK WDTF
- 同期テスト WDK WDTF
- 非同期テスト WDK WDTF
- テストスクリプト WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2cd4cfbfd27f5454972005ae5048bfef223b982
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841668"
---
# <a name="controlling-targets"></a>ターゲットの制御


WDTF には、ターゲットに対して特定のアクションを実行するインターフェイスのセットが含まれています。 WDTF は、Windows レジストリを使用して、これらのインターフェイスのターゲット固有の実装を実際のターゲットにマップします。 すべてのターゲット、または複数のクラス固有の実装に対して1つの実装が存在する場合があります。 シナリオでは、各ターゲットの詳細を把握しなくても、[**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/wdtf/action-interfaces)を使用して一般的なアクティビティを実行できます。

シナリオでは、 [**IWDTFTarget2:: GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)メソッドを呼び出すことによって、これらのインターフェイスのいずれかの実装を見つけることができます。 すべての対象オブジェクトがすべてのアクションインターフェイスをサポートするわけではないことに注意してください。 次の VBScript コード例では、ターゲットが表すデバイスを無効にして有効にできるインターフェイスを取得します。

```cpp
Set Action = Device.GetInterface("PNP")
```

[**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、Wdtf *ProgId*で識別されます。 [**Hasinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-hasinterface)、 [**getinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)、 [**getinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)、および[**GetInterfacesIfExist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)メソッドを呼び出すときには、wdtf *ProgId*を指定する必要があります。 WDTF *ProgId*の詳細については、「**アクションインターフェイス**」を参照してください。

プラグインモデルを使用して、インターフェイスのインターフェイスと実装を WDTF に追加できます。 このモデルの詳細については、「[フレームワークの拡張](extending-the-framework.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[フレームワークの拡張](extending-the-framework.md)  
[**GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)  
[**GetInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)  
[**GetInterfacesIfExist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)  
[**HasInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-hasinterface)  



