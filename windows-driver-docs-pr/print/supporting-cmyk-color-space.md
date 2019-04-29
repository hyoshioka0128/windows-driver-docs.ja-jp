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
ms.openlocfilehash: 519d8de97a7d8c70cf553b5b6eaa1db9d5ee707d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331756"
---
# <a name="supporting-cmyk-color-space"></a>CMYK 色領域をサポートする





関係なくかどうかの色の管理を処理しているアプリケーション、システム、ドライバー、またはデバイス、プリンター グラフィックス DLL 色空間。 これは、設定、GCAPS で\_打ち合わせますフラグ、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)構造体。 このフラグが設定され、CMYK プロファイルが使用中は場合、GDI はビットマップ、ブラシ、およびペンのプリンター グラフィックス DLL に RGB のデータではなく、CMYK カラー データを送信します。 GDI では、次のフラグも設定します。

-   BR\_打ち合わせますフラグ、 **flColorType**のメンバー、 [ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)構造体。

-   XO\_FROM\_CMYK フラグ、 **flXlate**のメンバー、 [ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)構造体。

ドライバーは CMYK カラー領域をサポートする場合はハーフトーンをサポートしているもする必要がありますに注意してください。 したがって、ドライバーの設定、GCAPS 場合\_打ち合わせますフラグ DEVINFO で、GCAPS を設定がありますも\_ハーフトーン。

 

 




