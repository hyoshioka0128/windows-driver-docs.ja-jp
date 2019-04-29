---
title: 作業の GDI/ドライバー分割
description: 作業の GDI/ドライバー分割
ms.assetid: 280addc6-3fc2-4763-ba87-5e9c5e83d22e
keywords:
- GDI WDK Windows 2000 の表示、人件費のドライバーの除算
- グラフィック ドライバー WDK Windows 2000 を表示する作業のドライバーの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a145a618f69ff4649bdabea2760d5548341401e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389095"
---
# <a name="gdidriver-division-of-labor"></a>作業の GDI/ドライバー分割


## <span id="ddk_gdi_2f_driver_division_of_labor_gg"></span><span id="DDK_GDI_2F_DRIVER_DIVISION_OF_LABOR_GG"></span>


グラフィックス ドライバーの設計を理解するのには、GDI と、ドライバーとそれらのネゴシエートの役割を理解する必要があります。 GDI や機能の強化と、グラフィックス ドライバーが必要だった多くの操作を処理できます。 GDI では、各グラフィック ドライバーはそれらへのアクセスがある必要ですが、サーフェスなどのグラフィックスの運営にとって重要なデータ構造を管理する責任もあります。

 

 





