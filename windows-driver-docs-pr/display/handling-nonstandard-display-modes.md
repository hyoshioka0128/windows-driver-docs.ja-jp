---
title: 非標準の表示モードの処理
description: 非標準の表示モードの処理
ms.assetid: 4a3b0064-46d4-40bb-b49b-ac172012a7b7
keywords:
- 非標準の表示モード WDK DirectX 9.0、処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07f25cfe1934bc763b498c9f4b5d06c8e8adef8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838909"
---
# <a name="handling-nonstandard-display-modes"></a>非標準の表示モードの処理


## <span id="ddk_handling_nonstandard_display_modes_gg"></span><span id="DDK_HANDLING_NONSTANDARD_DISPLAY_MODES_GG"></span>


非標準の表示モードをサポートするデバイスの DirectX 9.0 ドライバーでは、非標準モードを使用して次の操作も処理する必要があります。

-   標準表示モードと同じように動作するフリップ、array.blit、lock、および unlock 操作。

-   DirectX プライマリサーフェイスがアクティブなときに、ドライバーのグラフィックスデバイスインターフェイス (GDI) 関数を呼び出します。

    DirectX プライマリがアクティブになっている間、ドライバーは GDI DDI 描画呼び出しを受け取ることはできません。 ただし、ドライバーは、オペレーティングシステムがクラッシュすることなく、このような描画を処理する必要があります。 ドライバーは、このような状況の実装を提供したり、成功を直ちに返すことによって無視したり、失敗したりすることができます。 GDI のデータは、GDI のプライマリサーフェイス形式に基づいていることに注意してください。 このため、ドライバーがこのような状況の実装を提供する場合は、DirectX プライマリサーフェイスに描画する前に GDI 形式から変換する必要があります。

-   GDI が非標準の表示形式にアクセスできないため、DirectX プライマリサーフェイスに対する GDI DDI *DrvDeriveSurface*関数の呼び出しは発生しません。

-   DirectX プライマリサーフェイスがアクティブなときに「Ctl + Alt + Del」と入力します。

    カーネルでは、GDI の描画が行われる前に、ドライバーの[*Ddflip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)関数の呼び出しでターゲットとして標準プライマリが指定されています。 そのため、ドライバーは、GDI 描画の前にディスプレイデバイスを標準表示モードにプログラミングする必要があります。 プライマリサーフェイスのドライバーの[*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)関数も呼び出されます。 ドライバーは DirectX プライマリサーフェイスの内容を破棄できることに注意してください。

-   ウィンドウモードと非標準の形式

    「 [Surface 形式を使用した2D 操作のレポートのサポート](reporting-support-for-2d-operations-using-surface-formats.md)」トピックでは、ドライバーが、現在のデスクトップとは異なる形式のイメージのレンダリングを実行できることを指定する方法について説明します。 このスキームは、非標準の形式をサポートするために自然に拡張されるものです。ドライバーは、形式に対して、 [**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造体の**dwoperations**メンバーに有効化フラグを追加するだけである必要があります。

プライベート形式とレガシコードは、非標準のデスクトップ形式を公開するためには使用できません。

 

 





