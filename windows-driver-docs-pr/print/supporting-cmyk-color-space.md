---
title: CMYK 色領域をサポートする
description: CMYK 色領域をサポートする
ms.assetid: b8ac5f1a-c903-4313-b7de-0335f4c44367
keywords:
- CMYK カラー領域 WDK の印刷
- BR_CMYKCOLOR
- XO_FROM_CMYK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d8265864dce8a711d202a8fe6396a074a46e0be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354463"
---
# <a name="supporting-cmyk-color-space"></a>CMYK 色領域をサポートする





関係なくかどうかの色の管理を処理しているアプリケーション、システム、ドライバー、またはデバイス、プリンター グラフィックス DLL 色空間。 これは、設定、GCAPS で\_打ち合わせますフラグ、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。 このフラグが設定され、CMYK プロファイルが使用中は場合、GDI はビットマップ、ブラシ、およびペンのプリンター グラフィックス DLL に RGB のデータではなく、CMYK カラー データを送信します。 GDI では、次のフラグも設定します。

-   BR\_打ち合わせますフラグ、 **flColorType**のメンバー、 [ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)構造体。

-   XO\_FROM\_CMYK フラグ、 **flXlate**のメンバー、 [ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)構造体。

ドライバーは CMYK カラー領域をサポートする場合はハーフトーンをサポートしているもする必要がありますに注意してください。 したがって、ドライバーの設定、GCAPS 場合\_打ち合わせますフラグ DEVINFO で、GCAPS を設定がありますも\_ハーフトーン。

 

 




