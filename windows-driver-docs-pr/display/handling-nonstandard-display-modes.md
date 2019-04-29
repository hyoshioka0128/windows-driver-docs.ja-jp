---
title: 非標準の表示モードの処理
description: 非標準の表示モードの処理
ms.assetid: 4a3b0064-46d4-40bb-b49b-ac172012a7b7
keywords:
- WDK DirectX 9.0、処理の非表示モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54bb8c5a64a372260bc8ebd24e5f04ef44ab75df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323800"
---
# <a name="handling-nonstandard-display-modes"></a>非標準の表示モードの処理


## <span id="ddk_handling_nonstandard_display_modes_gg"></span><span id="DDK_HANDLING_NONSTANDARD_DISPLAY_MODES_GG"></span>


非標準の表示モードをサポートするデバイス用の DirectX 9.0 ドライバーでは、その非標準モードを使用して、次の操作を処理する必要がありますも。

-   反転、ブリット、ロック、および標準的な表示モードと同様に動作する操作のロックを解除します。

-   DirectX プライマリ画面がアクティブな間に、ドライバーのグラフィックス デバイス インターフェイス (GDI) 関数の呼び出し。

    ドライバーは、描画呼び出しの DirectX のプライマリがアクティブな間、GDI DDI を受信しませんする必要があります。 ただし、ドライバーは、オペレーティング システムがクラッシュを発生させることがなくこのような描画を処理する必要があります。 ドライバーでは、このような状況の実装を提供、すぐに成功すると、返すことによって無視、または失敗することができます。 GDI からデータを GDI のプライマリ画面形式に基づくことに注意してください。 そのため、ドライバーでは、このような状況の実装を提供する場合する必要があります形式から変換、GDI 描画前に、DirectX プライマリ画面を。

-   GDI DDI への呼び出し*DrvDeriveSurface* DirectX プライマリ画面に対して関数は、GDI が非標準の表示形式にアクセスできないために発生することはできません。

-   DirectX プライマリ画面がアクティブな間は、"Ctl + Alt + Del"を入力します。

    カーネル ドライバーの呼び出しでターゲットとして、標準のプライマリを指定する[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306) GDI 描画が行われる前に機能します。 そのため、ドライバーは、GDI 描画前に、標準の表示モードをディスプレイ デバイスをプログラミングする必要があります。 ドライバーの[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)関数のプライマリ画面と呼ばれます。 ドライバーが、DirectX プライマリ画面の内容を破棄できますに注意してください。

-   ウィンドウ表示モードと非標準の形式

    [2D 操作を使用して画面の形式のレポート作成のサポート](reporting-support-for-2d-operations-using-surface-formats.md)トピックでは、ドライバーが、現在のデスクトップとは異なる形式にレンダリングおよび存在するイメージを実行できることを指定する方法について説明します。 このスキームは非標準形式をサポートするために自然な拡張します。ドライバーがで有効にするフラグを追加する必要がありますだけで、 **dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)形式の構造体。

非標準のデスクトップの形式を公開する、プライベートな形式と古いコードを使用できません。

 

 





