---
title: プリンター固有の情報を返す
description: プリンター固有の情報を返す
ms.assetid: 7a47b395-4b01-437f-bed7-967b31b5841e
keywords:
- プリンター グラフィックス DLL の WDK には、プリンターに固有の情報が返されます。
- グラフィックス DLL WDK のプリンターはプリンターに固有の情報を返す
- WDK プリンター グラフィックス プリンター固有の情報を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48ae30a4f2c45c07875f09e9722dd6fec709da8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382558"
---
# <a name="returning-printer-specific-information"></a>プリンター固有の情報を返す





GDI がこのようなを呼び出すことによって印刷ジョブをプリンター グラフィックスをプリンターに固有の情報を返す間に DLL を要求して場合があります**DrvQuery**のプレフィックスとしてグラフィックス DDI 関数[ **DrvQueryAdvanceWidths** ](https://msdn.microsoft.com/library/windows/hardware/ff556259) (グラフィックス DLL によって定義される) 場合。

この現象が発生した場合の例では、印刷可能ページの WYSIWYG 画面表示の維持は、ワード プロセッシング アプリケーションの場合です。 テキストの改行を正しく表示するには、ワード プロセッサでは文字の幅とフォントの選択したプリンターの実装から他のフォント メトリック ベース ライン調整計算をする必要があります。

 

 




