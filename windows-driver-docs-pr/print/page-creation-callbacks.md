---
title: ページ作成コールバック
description: ページ作成コールバック
ms.assetid: ec514d17-415e-417b-bb29-b37be43c3cf6
keywords:
- WDK CPSUI のコールバック関数
- 共通のプロパティ シートのユーザー インターフェイスの WDK の印刷、コールバック
- CPSUI WDK の印刷、コールバック
- WDK プロパティ シートのページを印刷するコールバック
- ページの作成のコールバックを WDK CPSUI
- CommonPropertySheetUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f0acb8e4d854044fc975e44653e8e9dabd3be4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360726"
---
# <a name="page-creation-callbacks"></a>ページ作成コールバック





アプリケーションが関数をポイント CPSUI のエントリに初期呼び出しを行うときに ([**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)) のアドレスを含める必要があります、 [ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-コールバック関数を入力します。 このコールバック関数は、プロパティ シートのページを記述して作成の CPSUI にこれらの説明を送信します。

CPSUI の**CommonPropertySheetUI**関数がすぐに PFNPROPSHEETUI に型指定された関数のアドレス指定するのにはコールバックを[ **PROPSHEETUI\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_propsheetui_info)構造体。 アプリケーションには、CPSUI を呼び出して[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet) CPSUI は、次の図に示すように、ページの作成に使用できるページの説明を指定して、関数。

![アプリケーション cpsui 通信を示す図](images/comprop.png)

詳細については、次を参照してください。[メソッドを指定するページの](methods-for-specifying-pages.md)します。

 

 




