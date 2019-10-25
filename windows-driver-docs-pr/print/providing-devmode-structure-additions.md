---
title: DEVMODE 構造体の追加の提供
description: DEVMODE 構造体の追加の提供
ms.assetid: 7ce698f5-14c7-484d-be3d-b41c690b9576
keywords:
- ユーザーインターフェイスプラグイン WDK print、DEVMODEW 構造体の追加
- UI プラグイン WDK print、DEVMODEW 構造体の追加
- DEVMODEW
- プライベート DEVMODE WDK 印刷
- パブリック DEVMODE の WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c672b63dc5a671c32724b2abd4b269389addca2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840422"
---
# <a name="providing-devmode-structure-additions"></a>DEVMODE 構造体の追加の提供





UI プラグインは、次の図に示すように、独自のプライベートメンバーを[**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体に追加できます。

![パブリックとプライベートの devmode セクションを示す図](images/dvmdstru.png)

UI プラグインは、これらのプライベート DEVMODE メンバーを使用して、カスタマイズされたプリンターオプションに関連付けられている値を格納できます。 このプラグインを使用すると、ドライバーによって提供される[プロパティシートページを変更](modifying-a-driver-supplied-property-sheet-page.md)したり、[新しいプロパティシートページを追加](adding-new-property-sheet-pages.md)したりすることによって、ユーザーがこれらのオプションを使用できるようになります。

UI プラグインがプライベート DEVMODE メンバーを追加する場合、 [**OEM\_DMEXTRAHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oem_dmextraheader)構造体は、追加されたメンバーの前にプレフィックスを付ける必要があります。

DEVMODE 構造体にメンバーを追加する必要はありませんが、その場合、UI プラグインは[**Iprintoemui::D evMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode)メソッドを実装する必要があります。 このメソッドの目的は、入力引数に応じて、追加の DEVMODE メンバーのサイズを返す、初期化、変換、または検証します。

 

 




