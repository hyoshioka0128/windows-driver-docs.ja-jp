---
title: フレームワーク オブジェクトの概要
description: フレームワーク オブジェクトの概要
ms.assetid: 1314501a-bff1-4aac-a391-a72acca9cc26
keywords:
- フレームワーク オブジェクト WDK KMDF、framework のオブジェクトの概要
- 参照カウントの WDK KMDF
- 削除コールバック関数 WDK KMDF
- WDK KMDF のコールバック関数
- 親オブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e39e299c893e37221936f050a8e3f3fae771df3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371126"
---
# <a name="introduction-to-framework-objects"></a>フレームワーク オブジェクトの概要





ドライバーを Windows Driver Frameworks (WDF) を提供するインターフェイスでは、オブジェクト ベースです。 フレームワークは、いくつかのオブジェクトを定義します。 これらのオブジェクトのエクスポート[メソッド](framework-object-methods.md)(関数) と[プロパティ](framework-object-properties.md)(データ) ドライバーにアクセスできるようにします。 開始することも framework オブジェクト[イベント](framework-object-events.md)イベントのコールバック関数を提供することでどのドライバーをサポートできます。

フレームワーク ベースのドライバー決してオブジェクトに直接アクセス フレームワーク。 代わりに、ドライバーは参照によってオブジェクト*ハンドル*ドライバーは、オブジェクトのメソッドへの入力として渡されます。

フレームワークのすべてのオブジェクトには、次の特性があります。

<a href="" id="reference-count"></a>*参照カウント*  
フレームワークは、各オブジェクトへの参照の数のカウントを保持します。 フレームワークは、オブジェクトを作成するときに、1 つに、オブジェクトの参照カウントを設定します。 オブジェクトを使用して、フレームワークが完了すると、参照カウントをデクリメントします。 フレームワークは、ドライバーは、参照カウントをインクリメントして、オブジェクトの削除を防ぐことができますので、参照カウントがゼロにデクリメントされるまで、オブジェクトを削除できません。

<a href="" id="context-space"></a>*コンテキストの領域*  
フレームワーク ベースのドライバーがドライバーの受信または作成するすべての framework オブジェクトのオブジェクト固有のコンテキストの領域を作成できます。 ドライバーは、オブジェクトのコンテキストの領域で、すべてのオブジェクトに固有のデータを格納する必要があります。 コンテキストの領域に関する詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

<a href="" id="deletion-callback-functions"></a>*削除コールバック関数*  
ドライバーは、オブジェクトを削除するには、ときにフレームワークから呼び出されるコールバック関数を登録できます。 コールバック関数では、オブジェクト固有のメモリの割り当てなどのドライバーによって割り当てられたリソースを削除できます。 これらのコールバック関数の詳細については、次を参照してください。 [Framework オブジェクトのライフ サイクル](framework-object-life-cycle.md)します。

<a href="" id="parent-object"></a>*親オブジェクト*  
フレームワークのすべてのオブジェクトには、親オブジェクトを持つことができます。 フレームワークは、ほとんどのオブジェクトの既定の親オブジェクトを指定します。 ドライバーは、オブジェクトを作成するときに、オブジェクトの既定の親オブジェクトをオーバーライドする親オブジェクトを指定できます。 オブジェクトの親オブジェクトをドライバーのセットを指定する、 **ParentObject**オブジェクトのメンバー [ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体。 (いくつかのオブジェクトの種類のドライバーを上書きできません既定の親オブジェクト。)フレームワークまたはドライバーは、親オブジェクトを削除したときに、フレームワークには、親オブジェクトの子も削除されます。

すべての WDF で定義されているオブジェクトの概要については、次を参照してください。 [Framework オブジェクトの概要](summary-of-framework-objects.md)します。

 

 





