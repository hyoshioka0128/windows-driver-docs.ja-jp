---
title: コレクションの機能
description: コレクションの機能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- コレクションの WDK を非表示の機能
- WDK の HID 概要機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54f6fb798b3c8647edba1bf7192814627acd3360
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390342"
---
# <a name="collection-capability"></a>コレクションの機能





コレクションの機能は、その使用状況、レポート、リンクのコレクション、およびコントロールによって定義されます。 ユーザー モード アプリケーションまたはカーネル モード ドライバーを呼び出し、コレクションの機能の概要を取得する[ **HidP\_GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539715)を取得する、 [ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)構造体。 この構造体には、コレクションの詳細については、次の情報が含まれています[コレクションをリンク](link-collections.md)、[機能の配列をボタン](button-capability-arrays.md)、と[機能配列値](value-capability-arrays.md):。

-   コレクションの[使用状況 ページ](hid-usages.md#usage-page)と[使用状況 ID](hid-usages.md#usage-id)

-   コレクションのバイト単位のサイズが入力の出力、および機能の報告 (を参照してください[HID 概念の紹介](introduction-to-hid-concepts.md))

-   数[ **HIDP\_リンク\_コレクション\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff539764)構造、コレクションの[リンク コレクションの配列](link-collections.md#ddk-link-collection-array-kg)

-   各レポートの種類の数の[ **HIDP\_ボタン\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539693)ボタンの機能の配列内の構造がによって返される[ **HidP\_GetButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539707)

-   各レポートの種類の数の[ **HIDP\_値\_CAP**](https://msdn.microsoft.com/library/windows/hardware/ff539832)によって返される値の機能の配列内の構造体[ **HidP\_GetValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539754)

-   各レポートの種類のボタンとを指定して、コレクションによってサポートされる値の数、**数***Xxx***DataIndices**メンバー。

 

 




