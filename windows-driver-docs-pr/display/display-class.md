---
title: 表示クラス
description: スレッド処理と同期の最初のレベルでクラス DDIs を表示します。
ms.assetid: 439263ec-b28f-41ca-9c69-095216d63f38
keywords:
- ディスプレイドライバー WDK ウィンドウ、表示クラス
- スレッド処理と同期の第1レベル
ms.date: 04/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62ff92b01e0b0ca6d0cba3516d61faa177813b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838993"
---
# <a name="display-class"></a>表示クラス

Windows Display Driver Model (WDDM) では、表示クラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で次のいずれかの関数内で実行できます。

-   [*DxgkDdiSetTargetGamma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetgamma)

-   [*DxgkDdiSetTargetContentType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetcontenttype)

-   [*DxgkDdiSetTargetAnalogCopyProtection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetanalogcopyprotection)

-   [*DxgkDdiSetTargetAdjustedColorimetry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry)
