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
ms.openlocfilehash: a8ac765e8dfc4963f45d7fcc434ea102ede65b08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574437"
---
# <a name="page-creation-callbacks"></a>ページ作成コールバック





アプリケーションが関数をポイント CPSUI のエントリに初期呼び出しを行うときに ([**CommonPropertySheetUI**](https://msdn.microsoft.com/library/windows/hardware/ff546148)) のアドレスを含める必要があります、 [ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-コールバック関数を入力します。 このコールバック関数は、プロパティ シートのページを記述して作成の CPSUI にこれらの説明を送信します。

CPSUI の**CommonPropertySheetUI**関数がすぐに PFNPROPSHEETUI に型指定された関数のアドレス指定するのにはコールバックを[ **PROPSHEETUI\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff561767)構造体。 アプリケーションには、CPSUI を呼び出して[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207) CPSUI は、次の図に示すように、ページの作成に使用できるページの説明を指定して、関数。

![アプリケーション cpsui 通信を示す図](images/comprop.png)

詳細については、[メソッドを指定するページの](methods-for-specifying-pages.md)を参照してください。

 

 




