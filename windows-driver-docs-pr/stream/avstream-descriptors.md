---
title: AVStream の記述子
description: AVStream の記述子
ms.assetid: fd436406-311b-4537-994d-fbd8d92d4673
keywords:
- AVStream 記述子 WDK
- 記述子 WDK AVStream
- 入れ子になった記述子構造の WDK AVStream
- AVStream オブジェクト階層 WDK
- オブジェクト WDK AVStream
- 階層の WDK AVStream
- 静的記述子テーブル WDK AVStream
- KSFILTER_DESCRIPTOR
- デバイス記述子 WDK AVStream
- フィルターファクトリ WDK AVStream
- フィルターの種類 WDK AVStream
- pin の種類 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5903e543ddbf2a08f1fb3315e745689cccec4d13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845016"
---
# <a name="avstream-descriptors"></a>AVStream の記述子





AVStream ミニドライバーは、それ自体と、 [**Ksk Initializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)への呼び出しに入れ子になった記述子構造を提供することによってサポートされるフィルターの種類を記述します。 各主要コンポーネント (デバイス、[フィルターファクトリ](https://docs.microsoft.com/windows-hardware/drivers/audio/filter-factories)、および[pin ファクトリ](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-factories)) には、関連付けられた記述子があります。

[Avstream オブジェクト階層](avstream-object-hierarchy.md)に示されているように、avstream ミニドライバーの最上位レベルの記述子は、デバイス記述子、 [**KSDEVICE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)です。

デバイス記述子で、 **FilterDescriptors**メンバーは、このデバイスが作成できるフィルターの種類を記述する ksk フィルター\_記述子構造体の配列を指します。 AVStream クライアントは、フィルターファクトリを動的に追加するために[**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)を呼び出すことができます。

KSK フィルター\_記述子は、フィルターがサポートする pin の種類の数、フィルターを登録する必要がある KS のカテゴリ、およびフィルターのトポロジを示します。 各フィルター記述子の内部で、ミニドライバーは[**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の配列へのポインターを提供します。 これらの各 pin 記述子は、このフィルターがインスタンス化できる pin の種類を表します。 追加の pin ファクトリを作成するには、 [**Ksk Filtercreatepinfactを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltercreatepinfactory)呼び出します。

通常、AVStream ミニドライバーは、ソース内の静的な記述子テーブルをレイアウトし、 [**Ksk Initializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)を呼び出してセットアップ作業を実行します。 ドライバーの初期化の詳細については、「 [AVStream ミニドライバーの初期化](initializing-an-avstream-minidriver.md)」を参照してください。

その他の種類の記述子もあります。たとえば、ノード記述子[**ksnode\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)は、特定のトポロジノードを記述します。

ディスパッチテーブルは、3つの主要な記述子型のそれぞれに共通です。 [Avstream のディスパッチテーブル](avstream-dispatch-tables.md)を参照してください。

 

 




