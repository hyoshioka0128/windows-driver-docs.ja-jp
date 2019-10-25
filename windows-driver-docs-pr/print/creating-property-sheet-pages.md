---
title: プロパティ シート ページを作成する
description: プロパティ シート ページを作成する
ms.assetid: 90b1743c-b530-408a-aa30-9ab774166306
keywords:
- 一般的なプロパティシートのユーザーインターフェイス WDK 印刷、プロパティシートページの作成
- CPSUI WDK print、プロパティシートページの作成
- プロパティシートページ WDK 印刷、作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32903e345bb331f239907ba26df44fa28e43ca03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842851"
---
# <a name="creating-property-sheet-pages"></a>プロパティ シート ページを作成する





CPSUI を使用して作成されたプロパティシートのページは、[プロパティシートのオプション](property-sheet-options.md)で構成されます。各オプションは、ユーザーが変更可能な値を表します。 プロパティシートオプションのダイアログは、ユーザーがオプションの値を変更できるようにする、 [CPSUI でサポートされているウィンドウコントロール](cpsui-supported-window-controls.md)のセットを使用して作成されます。

CPSUI によって提供されるウィンドウコントロールは、 [CPSUI が提供するページとテンプレート](cpsui-supplied-pages-and-templates.md)内で表示できます。また、カスタマイズされたページで使用することもできます。 [ページを指定する方法](methods-for-specifying-pages.md)はいくつかありますが、そのすべてに CPSUI の[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数の呼び出しが含まれます。

プリンターと印刷ドキュメントのプロパティシートページを作成するには、[プリンタードライバーで CPSUI を使用](using-cpsui-with-printer-drivers.md)し、アプリケーション、印刷スプーラ、プリンターインターフェイス DLL、および CPSUI の間で対話を行う必要があります。

 

 




