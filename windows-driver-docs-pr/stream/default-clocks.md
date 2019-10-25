---
title: 既定のクロック
description: 既定のクロック
ms.assetid: 8c1a51e5-238b-446a-8f20-3fe1b82020b5
keywords:
- 既定のクロック WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 224e4847d0ed7f9026589df970e1bd91a5577e7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837718"
---
# <a name="default-clocks"></a>既定のクロック





カーネルストリーミングミニドライバーは、 [**KsAllocateDefaultClockEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclockex)を呼び出して、既定のクロック構造の割り当てと初期化を行うことができます。 または、 [**KsAllocateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclock)を呼び出すこともできます。これは、非クロックメンバーの既定のパラメーターを持つ**KsAllocateDefaultClockEx**のラッパーです。 **KsAllocateDefaultClockEx**を使用して既定のクロックを初期化した後、 [**KsCreateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultclock)を呼び出します。

既定のクロックでは、 [Ksk Propsetid\_clock](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)がサポートされており、フィルターの pin によって示される他の時計と同様にアクセスできます。 ただし、基になるデータ構造は、フィルターのピンによって作成され、そのピンと作成されたクロックのインスタンスによって共有されます。 クロックは、pin に依存して、共有構造内の現在の状態およびその他の要素を更新します。 既定のクロックは、通知要求とクロッククエリを処理します。

このクロックを提供するフィルターのピンにマスタークロックが割り当てられている場合、pin はこのクロックを所有します。 Pin は、他のクロック実装が割り当てられている場合と同様に、クロックファイルオブジェクトを参照する必要があります。 インスタンスの作成時に、既定のクロックでは pin のファイルオブジェクトが参照されません。 代わりに、共通クロック構造の初期割り当てと、クロックで開かれた各ファイルオブジェクトに基づいて、内部参照カウントを保持します。 クロックの所有者がクロック構造体を解放した場合でも、すべてのファイルオブジェクトが閉じられるまで、その状態は維持されます。 Pin は、標準クロックインターフェイスを経由するのではなく、既定のクロックオブジェクトに直接アクセスできます。

ミニドライバーでは、 [**Ksk プロパティ\_CLOCK\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-functiontable)プロパティをサポートしているため、ユーザーモードクライアントに参照クロック時間をチェックするメカニズムを提供できます。 このプロパティは、これを有効にする関数ポインターを構造体に格納します。これにより、正確なレート一致がサポートされます。

また、ミニドライバーでは、指定された pin で速度の変更が許可される場合に、 [**Ksk プロパティ\_STREAM\_rate**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-rate)プロパティをサポートしています。

カーネルストリーミングプロキシインターフェイスを使用するアプリケーションは、 [IKsClockPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-iksclockpropertyset)インターフェイスのメソッドを呼び出して、別の場所で使用される可能性のある物理クロックの時間を取得して設定します。

関連情報については、「[品質管理](quality-management.md)」を参照してください。

 

 




