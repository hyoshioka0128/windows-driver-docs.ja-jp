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
ms.openlocfilehash: e34d3494cb46325580c4ee4d1a24c45efe4950ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341315"
---
# <a name="group-parent"></a>グループ親





プロパティ シートのページは、1 つに割り当てて、化できます*グループの親*します。 親のグループを作成するには CPSUI を呼び出すことによって[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)関数と、 [ **CPSFUNC\_挿入\_PSUIPAGE**](https://msdn.microsoft.com/library/windows/hardware/ff546414)関数のコードと PSUIPAGEINSERT を指定する\_グループ\_として親、**型**のメンバー、 [ **INSERTPSUIPAGE\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff551634)構造体。

新しい親のグループが作成されたときにハンドルが返されます。 ハンドルとして使用できる、 *hComPropSheet*パラメーターを[ **ComPropSheet**](https://msdn.microsoft.com/library/windows/hardware/ff546207)を追加またはプロパティ シートのページを削除する場合、します。

さらに、グループの親ハンドルとして受信される、 **hComPropSheet**のメンバー、 [ **PROPSHEETUI\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff561767)によって受信される構造体、アプリケーションの[ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-コールバック関数を入力します。 新しいグループの親を作成しない場合、このプロパティ シートのすべてのページを割り当てる必要があります。

作成される各グループの親の下の追加のグループの親を作成することができます。 プロパティ シート自体は、最上位レベルのグループの親であると見なされます。 追加のグループの親を明示的に作成しない場合は、最上位の親に追加されたプロパティ シートのすべてのページが割り当てられます。

 

 




