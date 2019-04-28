---
title: BGR8888 から XR_BIAS への変換
description: BGR8888 から XR_BIAS への変換
ms.assetid: 53145cfe-d344-4242-b124-ddb507d876ad
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、XR_BIAS BGR8888 に変換します。
- 拡張形式 XR_BIAS BGR8888 に変換する、Windows 7 の WDK の表示
- BGR8888 を XR_BIAS WDK Windows 7 の表示に変換します。
- BGR8888 WDK Windows 7 の表示
- BGR8888 WDK Windows 7 の表示、XR_BIAS への変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9acd50bbd2bc5e56628e27d3f529f039fff17e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368630"
---
# <a name="conversion-from-bgr8888-to-xrbias"></a>BGR8888 から XR への変換\_バイアス


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

BGR8888 タイプの形式からの変換 (たとえば、DXGI\_形式\_B8G8R8A8\_UNORM) XR に\_バイアスとは、無損失。

510 のスケール ファクターが明示的に BGR8888 型形式と XR の間で明確に反転可能な変換を提供する選択\_511 のスケール ファクターによって出されるは 0.5 の近くの非線形のジャンプを発生せずにバイアスします。

 

 





