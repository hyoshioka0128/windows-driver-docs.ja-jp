---
title: ターゲットの制御
description: ターゲットの制御
ms.assetid: b329e9a2-7d24-4612-9aa1-9d7955a61473
keywords:
- Windows デバイスのテスト フレームワーク WDK、アクションのインターフェイス
- WDTF WDK、アクションのインターフェイス
- Windows デバイスのテスト フレームワーク WDK、管理しやすいテスト
- WDTF WDK、管理しやすいテスト
- 管理しやすいテスト WDK WDTF
- アクションは、WDK WDTF をインターフェイスします。
- COM インターフェイスの WDK WDTF
- WDK WDTF インターフェイス
- コード モジュール WDK WDTF
- WDK WDTF スクリプト
- 同期テスト WDK WDTF
- 非同期テスト WDK WDTF
- テスト スクリプト WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6cc73847ce6876bedba58888b0f472ee7052b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348036"
---
# <a name="controlling-targets"></a>ターゲットの制御


WDTF には、ターゲット上で特定のアクションを実行するインターフェイスのセットが含まれています。 WDTF では、Windows レジストリを使用して、実際のターゲットにこれらのインターフェイスのターゲット固有の実装をマップします。 すべてのターゲットまたは複数のクラスに固有の実装の 1 つの実装である可能性があります。 シナリオを使用できます[**アクション インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/wdtf/action-interfaces)各ターゲットの詳細を把握することも一般的なアクティビティを実行します。

これらのインターフェイスのいずれかの実装を呼び出すことによって検索しようとしてできます、シナリオ、 [ **IWDTFTarget2::GetInterface** ](https://msdn.microsoft.com/library/windows/hardware/hh439398)メソッド。 すべてのターゲット オブジェクトがすべてのアクションのインターフェイスをサポートすることに注意してください。 次の VBScript コード例は、インターフェイスを無効にして有効にすることができます (など) を取得します。 ターゲットを表すデバイス。

```cpp
Set Action = Device.GetInterface("PNP")
```

[**アクション インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff538355) 、WDTF で識別されます*ProgId*します。 WDTF を指定する必要があります*ProgId*を呼び出すと、 [ **HasInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439447)、 [ **GetInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439398)、[ **GetInterfaces**](https://msdn.microsoft.com/library/windows/hardware/hh439475)、および[ **GetInterfacesIfExist** ](https://msdn.microsoft.com/library/windows/hardware/hh439478)メソッド。 WDTF について*ProgId*を参照してください、**アクション インターフェイス**します。

WDTF をインターフェイスおよびインターフェイスの実装を追加するにはプラグイン モデルを使用します。 このモデルの詳細については、次を参照してください。[フレームワークを拡張する](extending-the-framework.md)します。

## <a name="related-topics"></a>関連トピック
[**アクションのインターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff538355)  
[フレームワークを拡張します。](extending-the-framework.md)  
[**GetInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439398)  
[**GetInterfaces**](https://msdn.microsoft.com/library/windows/hardware/hh439475)  
[**GetInterfacesIfExist**](https://msdn.microsoft.com/library/windows/hardware/hh439478)  
[**HasInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439447)  



