---
title: DEVMODE 構造の追加機能を提供する
description: DEVMODE 構造の追加機能を提供する
ms.assetid: 7ce698f5-14c7-484d-be3d-b41c690b9576
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、DEVMODEW 構造の追加
- UI プラグインを WDK の印刷、DEVMODEW 構造の追加
- DEVMODEW
- プライベート DEVMODE WDK の印刷
- パブリックの DEVMODE WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a89551be81348cf9bdd95529fc8b5ca02ca167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376572"
---
# <a name="providing-devmode-structure-additions"></a>DEVMODE 構造の追加機能を提供する





UI プラグインに独自のプライベート メンバーを追加、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)次の図に示すように、構造体します。

![パブリックおよびプライベートの devmode のセクションを示す図](images/dvmdstru.png)

UI のプラグインでは、カスタマイズされたプリンター オプションに関連付けられている値を格納するのにプライベートこれら DEVMODE のメンバーを使用できます。 プラグインこれらのオプションを使用できるように、ユーザーによって[ドライバーによって提供されるプロパティ シート ページを変更する](modifying-a-driver-supplied-property-sheet-page.md)または[新しいプロパティ シートのページを追加する](adding-new-property-sheet-pages.md)します。

UI プラグインは、プライベートの DEVMODE のメンバーを追加する場合、 [ **OEM\_DMEXTRAHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff559588)構造に追加されたメンバーを付ける必要があります。

DEVMODE 構造体にメンバーを追加する必要はありませんが、UI のプラグインを実装する必要がありますを行った場合、 [ **IPrintOemUI::DevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff554167)メソッド。 入力引数は、によって、このメソッドの目的は、サイズを返します、初期化、変換、またはその他の DEVMODE のメンバーを検証するのには。

 

 




