---
title: グループ親
description: グループ親
ms.assetid: b4c40c15-df16-4af0-81c8-9e70d26ba598
keywords:
- グループの親の WDK の印刷
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、グループの親
- CPSUI WDK の印刷、グループの親
- WDK プロパティ シートのページを印刷するグループの親
- プロパティ シートのページをグループ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b76cd1adf5357c4cc24179c21a20e21330ae2756
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368988"
---
# <a name="group-parent"></a>グループ親





プロパティ シートのページは、1 つに割り当てて、化できます*グループの親*します。 親のグループを作成するには CPSUI を呼び出すことによって[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)関数と、 [ **CPSFUNC\_挿入\_PSUIPAGE**](https://docs.microsoft.com/previous-versions/ff546414(v=vs.85))関数のコードと PSUIPAGEINSERT を指定する\_グループ\_として親、**型**のメンバー、 [ **INSERTPSUIPAGE\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_insertpsuipage_info)構造体。

新しい親のグループが作成されたときにハンドルが返されます。 ハンドルとして使用できる、 *hComPropSheet*パラメーターを[ **ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)を追加またはプロパティ シートのページを削除する場合、します。

さらに、グループの親ハンドルとして受信される、 **hComPropSheet**のメンバー、 [ **PROPSHEETUI\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_propsheetui_info)によって受信される構造体、アプリケーションの[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-コールバック関数を入力します。 新しいグループの親を作成しない場合、このプロパティ シートのすべてのページを割り当てる必要があります。

作成される各グループの親の下の追加のグループの親を作成することができます。 プロパティ シート自体は、最上位レベルのグループの親であると見なされます。 追加のグループの親を明示的に作成しない場合は、最上位の親に追加されたプロパティ シートのすべてのページが割り当てられます。

 

 




