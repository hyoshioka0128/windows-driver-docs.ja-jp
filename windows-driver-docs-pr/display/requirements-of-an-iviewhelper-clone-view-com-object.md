---
title: IViewHelper 複製ビュー COM オブジェクトの要件
description: IViewHelper 複製ビュー COM オブジェクトの要件
ms.assetid: ef599874-64c5-480e-a7bc-666ababd4d08
keywords:
- TMM WDK の表示、IViewHelper 要件
- モニターの構成の WDK 表示、IViewHelper 要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0adbda8fae172221a8a7789908c9bcaa1656552
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385661"
---
# <a name="requirements-of-an-iviewhelper-clone-view-com-object"></a>IViewHelper 複製ビュー COM オブジェクトの要件


ハードウェア ベンダーの複製-ビュー [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) COM インターフェイスのオブジェクトは、次の要件を満たす必要があります。

-   COM オブジェクトは、COM のプロセス (インプロセス) サーバーでは、ダイナミック リンク ライブラリ (DLL) 内に存在する必要があります。

-   COM オブジェクトの実装は、オペレーティング システムに対して非透過的である必要があります。

-   [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)インターフェイスが取得およびクローンのビューを含むトポロジのデータを設定する方法を指定する必要があります。

-   ハードウェア ベンダーは、表示が 2 つ以上のモニターに表示されるように、複製ビューの表示モードを見つける必要があります。

-   COM オブジェクトの呼び出し[ **IViewHelper::Commit** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドは、モードの変更を生成しません**コミット**Win32 を呼び出す必要があります**BroadcastSystemMessage**関数を常に投稿する必要があります (、個所を使用して\_POSTMESSAGE ブロードキャスト オプション)、WM\_DISPLAYCHANGE メッセージ。 詳細については**BroadcastSystemMessage**、Microsoft Windows SDK のドキュメントを参照してください。

-   [ **IViewHelper::Commit** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドは、Win32 への呼び出しの代わりに使用する必要があります**ChangeDisplaySettingsEx**(**NULL**、 **NULL**、 **NULL**, 0, **NULL**) 指定された引数で関数をします。 詳細については**ChangeDisplaySettingsEx**、Windows SDK のマニュアルを参照してください。

 

 





