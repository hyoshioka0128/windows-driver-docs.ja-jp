---
title: 既定のクロック
description: 既定のクロック
ms.assetid: 8c1a51e5-238b-446a-8f20-3fe1b82020b5
keywords:
- 既定のクロックの WDK カーネルがストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c17ac3da20cde10ba78d63ec48670800d4ce7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376378"
---
# <a name="default-clocks"></a>既定のクロック





カーネルのミニドライバーのストリーミングを呼び出すことができます[ **KsAllocateDefaultClockEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksallocatedefaultclockex)を割り当てたり、既定のクロックの構造体を初期化します。 代わりに、呼び出すことができます[ **KsAllocateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksallocatedefaultclock)、用のラッパーである**KsAllocateDefaultClockEx** nonclock メンバーの既定のパラメーターを使用します。 呼び出す[ **KsCreateDefaultClock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedefaultclock)を使用した後**KsAllocateDefaultClockEx**を既定の時刻を初期化します。

既定の時刻をサポートしています[KSPROPSETID\_クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)フィルターの暗証番号 (pin) によって提示されるその他の任意のクロックと同様にアクセスできますが。 基になるデータ構造、ただし、して、フィルターは、暗証番号 (pin)、によって作成されたがその pin と作成される、時計のインスタンスで共有される クロックは、現在の状態と共有の構造体の他の要素を更新するピンに依存します。 通知要求を処理する既定の時計と時計のクエリ。

このクロックを提供するフィルターで pin には、マスターのクロックが割り当てられている、ときに、暗証番号 (pin) には、このクロックが所有しています。 Pin は、その他のクロックの実装が割り当てられている場合と同様、クロック ファイル オブジェクトを参照する必要があります。 既定の時刻では、インスタンスが作成されたときに暗証番号 (pin) のファイル オブジェクトを参照していません。 代わりに、共通のクロックの構造の初期の割り当てと、クロックに開かれた各ファイル オブジェクトに基づいて、内部参照カウントを保持します。 クロックの所有者は、クロックの構造体を解放、場合でもすべてのファイル オブジェクトが閉じられるまでインプレースは残ります。 Pin できます直接、既定のクロック オブジェクトにアクセスではなくクロックの標準的なインターフェイスを経由します。

ミニドライバーがサポートできる、 [ **KSPROPERTY\_クロック\_FUNCTIONTABLE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-functiontable)参照クロックの時刻を確認するためのメカニズムをユーザー モードのクライアントに提供するプロパティ。 このプロパティは、正確な速度の一致をサポートしているため、これを有効にする関数のポインターを持つ構造体に格納します。

さらに、ミニドライバーのサポート、 [ **KSPROPERTY\_ストリーム\_レート**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-rate)プロパティの指定した pin がレートの変化を許可する場合。

メソッドの呼び出しは、カーネルがストリーミング プロキシ インターフェイスを使用するアプリケーション、 [IKsClockPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-iksclockpropertyset)インターフェイスを取得し、レートが一致する他の場所で使用できる物理クロックの時刻を設定します。

参照してください[品質管理](quality-management.md)関連情報についてはします。

 

 




