---
title: デバイス フォントのサポート
description: デバイス フォントのサポート
ms.assetid: 9ca3269d-3f87-4d8a-a897-7305ac172227
keywords:
- プリンター グラフィックス DLL WDK、デバイス フォント
- グラフィックス デバイス フォント、DLL の WDK プリンター
- デバイス フォント WDK プリンター グラフィックス
- フォント WDK プリンター グラフィックス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2430cd8a55c3121140bec15d20accc253552200f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354462"
---
# <a name="supporting-device-fonts"></a>デバイス フォントのサポート





デバイス フォントをプリンターに提供する場合、プリンター グラフィックス DLL する必要がありますを定義、 [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)コマンドの出力テキストを生成する関数。 グラフィックス DLL には、次の関数を定義もする必要があります。

[**DrvQueryAdvanceWidths**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryadvancewidths)
[**DrvQueryFont**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfont)
[**DrvQueryFontData**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata) 
 [ **DrvQueryFontTree** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree)デバイス フォントのサポートに関する詳細については、次を参照してください[をサポートしているグラフィックス DDI フォントとテキスト関数。](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-graphics-ddi-font-and-text-functions)

 

 




