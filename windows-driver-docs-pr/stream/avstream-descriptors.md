---
title: AVStream 記述子
description: AVStream 記述子
ms.assetid: fd436406-311b-4537-994d-fbd8d92d4673
keywords:
- AVStream 記述子 WDK
- WDK AVStream 記述子
- 入れ子になった記述子 WDK AVStream を構造体します。
- AVStream オブジェクト階層 WDK
- WDK AVStream オブジェクト
- WDK AVStream の階層
- 静的な記述子テーブル WDK AVStream
- KSFILTER_DESCRIPTOR
- デバイス記述子 WDK AVStream
- ファクトリ WDK AVStream をフィルター処理します。
- WDK AVStream の種類をフィルターします。
- WDK AVStream の種類をピン留め
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10cc2380f80be9c48f0fa2e8df28b500f8e59809
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538653"
---
# <a name="avstream-descriptors"></a>AVStream 記述子





AVStream、ミニドライバーは、それ自体について説明し、フィルターの型はサポートへの呼び出しで入れ子になった記述子構造体を提供することで[ **KsInitializeDriver**](https://msdn.microsoft.com/library/windows/hardware/ff562683)します。 各主要コンポーネント--、デバイス、[フィルター ファクトリ](https://msdn.microsoft.com/library/windows/hardware/ff536385)、および[pin ファクトリ](https://msdn.microsoft.com/library/windows/hardware/ff537747)--に関連付けられている記述子があります。

ように[AVStream オブジェクト階層](avstream-object-hierarchy.md)、AVStream ミニドライバーの最上位レベルの記述子は、デバイス記述子[ **KSDEVICE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff561691).

デバイス記述子で、 **FilterDescriptors** KSFILTER の配列を指すメンバー\_フィルターの種類を記述する記述子構造体このデバイスを作成できます。 AVStream クライアントが呼び出すことができます[ **KsCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff561650)を動的にフィルター ファクトリを追加します。

KSFILTER\_記述子では、pin の数、フィルターがサポートされるフィルターは、登録するには、KS カテゴリ、フィルターのトポロジの種類を示します。 各フィルター記述子内で、ミニドライバーの配列へのポインターを提供します[ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 これらのピン留めする記述子のそれぞれには、このフィルターをインスタンス化できる暗証番号 (pin) の種類について説明します。 追加の pin のファクトリを作成するには呼び出すことによって[ **KsFilterCreatePinFactory**](https://msdn.microsoft.com/library/windows/hardware/ff562529)します。

通常、AVStream ミニドライバー レイアウト、ソースと呼び出しの静的な記述子テーブル[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683)セットアップ作業を実行します。 ドライバーを初期化する方法についての詳細については、次を参照してください。 [、AVStream ミニドライバーの初期化](initializing-an-avstream-minidriver.md)します。

ノードの記述子などがある他の種類も、記述子の[ **KSNODE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563473)、特定のトポロジのノードについて説明します。

ディスパッチ テーブルは 3 つの主な記述子の種類のそれぞれに共通です。 参照してください[AVStream ディスパッチ テーブル](avstream-dispatch-tables.md)します。

 

 




