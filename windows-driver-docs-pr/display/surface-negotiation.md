---
title: サーフェス ネゴシエーション
description: サーフェス ネゴシエーション
ms.assetid: af368be6-ea32-49ea-b49e-7e3c9a30facb
keywords:
- ネゴシエーション WDK GDI を画面します。
- GDI WDK Windows 2000 の表示、サーフェス
- グラフィックス ドライバー WDK Windows 2000 の表示、セキュリティのネゴシエーション
- 描画 WDK GDI やサーフェスのネゴシエーション
- WDK GDI のネゴシエーション
- セキュリティ ネゴシエーションのネゴシエーション WDK の GDI サーフェス
- ビットマップ、GDI WDK Windows 2000 の表示
- ビットマップ グラフィックス ドライバー WDK Windows 2000 の表示
- WDK GDI、ビットマップの描画
- WDK GDI ビットマップ
- セカンダリ サーフェス WDK GDI
- オフスクリーン サーフェス WDK GDI
- プライマリ サーフェス WDK GDI
- WDK GDI のサーフェスを画面に表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c22a73ee8b98e8dd06513499e10c36f9142f864
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572464"
---
# <a name="surface-negotiation"></a>サーフェス ネゴシエーション


## <span id="ddk_surface_negotiation_gg"></span><span id="DDK_SURFACE_NEGOTIATION_GG"></span>


描画とテキストの出力には、サーフェイスを描画する必要があります。 この画面がによって作成された、 **DrvEnableSurface**ドライバーは、いくつか PDEVs をサポートできます。 サポートするドライバー、 [ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)関数は作成し、追加のサーフェスを使用します。 これらのビットマップ サーフェスと呼びます*セカンダリ サーフェス*または*オフスクリーン サーフェス*します。 画面のいずれかの種類のドライバーが、型を判断するの描画操作をサポートします。

 

 





