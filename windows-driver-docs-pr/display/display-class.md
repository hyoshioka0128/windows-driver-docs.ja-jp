---
title: クラスを表示します。
description: スレッドと同期の最初のレベルで Ddi クラスを表示します。
ms.assetid: 439263ec-b28f-41ca-9c69-095216d63f38
keywords:
- ディスプレイ ドライバー WDK Windows, クラスの表示
- スレッドと同期の最初のレベル
ms.date: 04/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33102ec6c3443929e4b18c6e26d8139376749522
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351466"
---
# <a name="display-class"></a>ディスプレイ クラス

Windows 表示 Driver Model (WDDM) は、再入可能な方法で、表示のクラスの関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiSetTargetGamma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetgamma)

-   [*DxgkDdiSetTargetContentType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetcontenttype)

-   [*DxgkDdiSetTargetAnalogCopyProtection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetanalogcopyprotection)

-   [*DxgkDdiSetTargetAdjustedColorimetry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry)
