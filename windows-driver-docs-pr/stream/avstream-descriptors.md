---
title: AVStream の記述子
description: AVStream の記述子
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
ms.openlocfilehash: c38d6a0c6bea452a832b95e338afd555aa665c07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386703"
---
# <a name="avstream-descriptors"></a>AVStream の記述子





AVStream、ミニドライバーは、それ自体について説明し、フィルターの型はサポートへの呼び出しで入れ子になった記述子構造体を提供することで[ **KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)します。 各主要コンポーネント--、デバイス、[フィルター ファクトリ](https://docs.microsoft.com/windows-hardware/drivers/audio/filter-factories)、および[pin ファクトリ](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-factories)--に関連付けられている記述子があります。

ように[AVStream オブジェクト階層](avstream-object-hierarchy.md)、AVStream ミニドライバーの最上位レベルの記述子は、デバイス記述子[ **KSDEVICE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor).

デバイス記述子で、 **FilterDescriptors** KSFILTER の配列を指すメンバー\_フィルターの種類を記述する記述子構造体このデバイスを作成できます。 AVStream クライアントが呼び出すことができます[ **KsCreateFilterFactory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatefilterfactory)を動的にフィルター ファクトリを追加します。

KSFILTER\_記述子では、pin の数、フィルターがサポートされるフィルターは、登録するには、KS カテゴリ、フィルターのトポロジの種類を示します。 各フィルター記述子内で、ミニドライバーの配列へのポインターを提供します[ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 これらのピン留めする記述子のそれぞれには、このフィルターをインスタンス化できる暗証番号 (pin) の種類について説明します。 追加の pin のファクトリを作成するには呼び出すことによって[ **KsFilterCreatePinFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfiltercreatepinfactory)します。

通常、AVStream ミニドライバー レイアウト、ソースと呼び出しの静的な記述子テーブル[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)セットアップ作業を実行します。 ドライバーを初期化する方法についての詳細については、次を参照してください。 [、AVStream ミニドライバーの初期化](initializing-an-avstream-minidriver.md)します。

ノードの記述子などがある他の種類も、記述子の[ **KSNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)、特定のトポロジのノードについて説明します。

ディスパッチ テーブルは 3 つの主な記述子の種類のそれぞれに共通です。 参照してください[AVStream ディスパッチ テーブル](avstream-dispatch-tables.md)します。

 

 




