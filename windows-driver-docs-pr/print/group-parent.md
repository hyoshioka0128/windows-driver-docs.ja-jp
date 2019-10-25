---
title: グループ親
description: グループ親
ms.assetid: b4c40c15-df16-4af0-81c8-9e70d26ba598
keywords:
- グループ親 WDK 印刷
- 共通プロパティシートのユーザーインターフェイス WDK print、グループの親
- CPSUI WDK print、グループの親
- プロパティシートページの WDK 印刷、グループの親
- プロパティシートのページをグループ化する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 000014b2ca770182027eb6398f0b60087062d8a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844577"
---
# <a name="group-parent"></a>グループ親





プロパティシートのページは、1つの*グループの親*に割り当ててグループ化することができます。 [**Cpsfunc\_INSERT\_PSUIPAGE**](https://docs.microsoft.com/previous-versions/ff546414(v=vs.85))関数コードを指定して CPSUI の[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数を呼び出し、PSUIPAGEINSERT\_Group\_parent を**型**のメンバーとして指定することによって、[**グループの親を作成できます。INSERTPSUIPAGE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_insertpsuipage_info)構造体。

新しいグループの親が作成されると、ハンドルが返されます。 このハンドルは、プロパティシートページを追加または削除するときに、 [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)の*hComPropSheet*パラメーターとして使用できます。

さらに、グループの親ハンドルは、アプリケーションの[**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)型のコールバック関数によって受信される[**PROPSHEETUI\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_propsheetui_info)構造体の**hComPropSheet**メンバーとして受信されます。 新しいグループの親を作成しない場合は、すべてのプロパティシートページをこのページに割り当てる必要があります。

作成される各グループの親の下に、追加のグループの親を作成できます。 プロパティシート自体は、最上位レベルのグループの親と見なされます。 追加のグループの親を明示的に作成しない場合は、追加されたすべてのプロパティシートページが最上位の親に割り当てられます。

 

 




