---
title: ページ作成コールバック
description: ページ作成コールバック
ms.assetid: ec514d17-415e-417b-bb29-b37be43c3cf6
keywords:
- コールバック関数 WDK CPSUI
- 共通プロパティシートのユーザーインターフェイス WDK print、コールバック
- CPSUI WDK print、コールバック
- プロパティシートページの WDK 印刷、コールバック
- ページ作成コールバックの WDK CPSUI
- CommonPropertySheetUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ac4a1ecc8de0ba1909d93c92d69c12ef7c6f1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845049"
---
# <a name="page-creation-callbacks"></a>ページ作成コールバック





アプリケーションが CPSUI のエントリポイント関数 ([**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)) への最初の呼び出しを行うときは、 [**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)型のコールバック関数のアドレスを含める必要があります。 このコールバック関数は、プロパティシートページを記述し、それらの説明を作成のために CPSUI に送信します。

CPSUI の**CommonPropertySheetUI**関数は、 [**PROPSHEETUI\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_propsheetui_info)構造体のアドレスを指定して、すぐに PFNPROPSHEETUI 型の関数にコールバックします。 次の図に示すように、アプリケーションでは、CPSUI の[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数を呼び出して、CPSUI がページの作成に使用できるページの説明を提供できます。

![アプリケーションと cpsui の通信を示す図](images/comprop.png)

詳細については、「[ページを指定するためのメソッド](methods-for-specifying-pages.md)」を参照してください。

 

 




