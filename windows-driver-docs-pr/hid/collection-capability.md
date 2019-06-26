---
title: コレクションの機能
description: コレクションの機能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- コレクションの WDK を非表示の機能
- WDK の HID 概要機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a396ebe313943520269c8f2c507659b99b7deb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375768"
---
# <a name="collection-capability"></a>コレクションの機能





コレクションの機能は、その使用状況、レポート、リンクのコレクション、およびコントロールによって定義されます。 ユーザー モード アプリケーションまたはカーネル モード ドライバーを呼び出し、コレクションの機能の概要を取得する[ **HidP\_GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getcaps)を取得する、 [ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)構造体。 この構造体には、コレクションの詳細については、次の情報が含まれています[コレクションをリンク](link-collections.md)、[機能の配列をボタン](button-capability-arrays.md)、と[機能配列値](value-capability-arrays.md):。

-   コレクションの[使用状況 ページ](hid-usages.md#usage-page)と[使用状況 ID](hid-usages.md#usage-id)

-   コレクションのバイト単位のサイズが入力の出力、および機能の報告 (を参照してください[HID 概念の紹介](introduction-to-hid-concepts.md))

-   数[ **HIDP\_リンク\_コレクション\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_link_collection_node)構造、コレクションの[リンク コレクションの配列](link-collections.md#ddk-link-collection-array-kg)

-   各レポートの種類の数の[ **HIDP\_ボタン\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_button_caps)ボタンの機能の配列内の構造がによって返される[ **HidP\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getbuttoncaps)

-   各レポートの種類の数の[ **HIDP\_値\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_value_caps)によって返される値の機能の配列内の構造体[ **HidP\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getvaluecaps)

-   各レポートの種類のボタンとを指定して、コレクションによってサポートされる値の数、**数***Xxx***DataIndices**メンバー。

 

 




