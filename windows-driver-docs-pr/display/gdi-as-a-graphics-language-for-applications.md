---
title: アプリケーションのグラフィックス言語として GDI
description: アプリケーションのグラフィックス言語として GDI
ms.assetid: fc824284-0400-47b0-ac4e-ff21e1e0ded9
keywords:
- GDI WDK Windows 2000 の表示、アプリケーションにグラフィックスの言語
- グラフィック ドライバー WDK Windows 2000、グラフィックの表示言語のアプリケーション
- WDK の GDI やアプリケーションに言語をグラフィックスの描画
- アプリケーション WDK の GDI グラフィックス言語
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e0738724ae028f131c93606806b357a771e640
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527849"
---
# <a name="gdi-as-a-graphics-language-for-applications"></a>アプリケーションのグラフィックス言語として GDI


## <span id="ddk_gdi_as_a_graphics_language_for_applications_gg"></span><span id="DDK_GDI_AS_A_GRAPHICS_LANGUAGE_FOR_APPLICATIONS_GG"></span>


Win32 GDI とグラフィックス エンジンは、完全にデバイスに依存しないが。 その結果、アプリケーションでは、ハードウェアに直接アクセスする必要はありません。 アプリケーションのグラフィックス要求に基づいて、GDI は、グラフィックス デバイスの配列の高品質なグラフィックスの出力を提供するデバイスに依存するグラフィックス ドライバーと組み合わせて動作します。 印刷と表示の両方のデバイスでは、同じ GDI コード パスが使用されます。

 

 





