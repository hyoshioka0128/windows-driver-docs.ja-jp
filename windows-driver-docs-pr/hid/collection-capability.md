---
title: コレクションの機能
description: コレクションの機能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- 機能 WDK HID コレクション
- 概要機能 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477888c224dca2ca8f075d6e649b1bd0d069c89d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824844"
---
# <a name="collection-capability"></a>コレクションの機能





コレクションの機能は、その使用、レポート、リンクコレクション、およびコントロールによって定義されます。 コレクションの機能の概要を取得するために、ユーザーモードのアプリケーションまたはカーネルモードドライバーは、 [**hidp\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)を呼び出して、 [**HIDP\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体を取得します。 この構造体には、コレクションの[リンクコレクション](link-collections.md)、[ボタン機能配列](button-capability-arrays.md)、および[値機能配列](value-capability-arrays.md)に関する次の情報が含まれています。

-   コレクションの [[使用状況] ページ](hid-usages.md#usage-page)と[使用状況 ID](hid-usages.md#usage-id)

-   コレクションの入力、出力、および機能レポートのサイズ (バイト単位) (「HID の[概念の概要」を](introduction-to-hid-concepts.md)参照)

-   コレクションの[リンクコレクション配列](link-collections.md#ddk-link-collection-array-kg)の[ **\_コレクション\_ノード構造の\_リンク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_link_collection_node)の数

-   各レポートの種類では、hidp [ **\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)によって返されたボタン機能の配列の[ **\_、hidp\_ボタン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_button_caps)の数がキャップ構造になります。

-   各レポートの種類について、hidp [ **\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)によって返された値機能配列の[ **\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)構造の\_の値の数。

-   各レポートの種類について、 **Number***Xxx***DataIndices**メンバーによって指定された、コレクションでサポートされているボタンと値の数。

 

 




