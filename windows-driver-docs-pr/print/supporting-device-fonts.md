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
ms.openlocfilehash: 11c07cfd3b1f1ace4b9d728e014a6ff182fc4783
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331760"
---
# <a name="supporting-device-fonts"></a>デバイス フォントのサポート





デバイス フォントをプリンターに提供する場合、プリンター グラフィックス DLL する必要がありますを定義、 [ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)コマンドの出力テキストを生成する関数。 グラフィックス DLL には、次の関数を定義もする必要があります。

[**DrvQueryAdvanceWidths**](https://msdn.microsoft.com/library/windows/hardware/ff556259)
[**DrvQueryFont**](https://msdn.microsoft.com/library/windows/hardware/ff556262)
[**DrvQueryFontData**](https://msdn.microsoft.com/library/windows/hardware/ff556264) 
 [ **DrvQueryFontTree** ](https://msdn.microsoft.com/library/windows/hardware/ff556266)デバイス フォントのサポートに関する詳細については、次を参照してください[をサポートしているグラフィックス DDI フォントとテキスト関数。](https://msdn.microsoft.com/library/windows/hardware/ff569868).

 

 




