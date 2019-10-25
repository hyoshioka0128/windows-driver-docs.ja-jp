---
title: IViewHelper 複製ビュー COM オブジェクトの要件
description: IViewHelper 複製ビュー COM オブジェクトの要件
ms.assetid: ef599874-64c5-480e-a7bc-666ababd4d08
keywords:
- TMM WDK display, IViewHelper の要件
- 監視構成 WDK display, IViewHelper の要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 750bd627aa864e3fdaa646a7bf1e9867942b2a61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825852"
---
# <a name="requirements-of-an-iviewhelper-clone-view-com-object"></a>IViewHelper 複製ビュー COM オブジェクトの要件


ハードウェアベンダーの複製ビュー [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスオブジェクトは、次の要件を満たしている必要があります。

-   COM オブジェクトは、COM インプロセス (インプロセス) サーバーであるダイナミックリンクライブラリ (DLL) 内に存在する必要があります。

-   COM オブジェクトの実装は、オペレーティングシステムに対して非透過的である必要があります。

-   [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)インターフェイスには、複製ビューを含むトポロジデータを取得および設定するためのメソッドが用意されている必要があります。

-   ハードウェアベンダーは、表示が2つ以上のモニターに表示されるように、複製ビューの表示モードを見つける必要があります。

-   COM オブジェクトの[**IViewHelper:: commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドの呼び出しでモードの変更が生成されない場合、 **Commit**は Win32 **BroadcastSystemMessage**関数を呼び出す必要があり、常に (BSF\_POSTMESSAGE broadcast オプションを使用して) WM を post する必要があり @noDISPLAYCHANGE メッセージ (_s)。 **BroadcastSystemMessage**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

-   指定された引数を使用して、Win32 **Changedisplaysettingsex**(**null**、 **null**、 **null**、0、 **Null**) 関数への呼び出しの代わりに[**IViewHelper:: Commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドを使用することはできません。 **Changedisplaysettingsex**の詳細については、Windows SDK のドキュメントを参照してください。

 

 





