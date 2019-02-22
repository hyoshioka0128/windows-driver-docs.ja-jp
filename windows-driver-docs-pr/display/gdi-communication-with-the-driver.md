---
title: ドライバーとの通信を GDI
description: ドライバーとの通信を GDI
ms.assetid: 81d9e87f-883b-4019-86fc-bccde861de46
keywords:
- GDI WDK Windows 2000 の表示、ドライバーの通信
- グラフィックス ドライバー WDK Windows 2000 の表示、ドライバーの通信
- 描画 WDK GDI やドライバーの通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35905c02d622b0e31c1aaedf6d25190361cfa1a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537024"
---
# <a name="gdi-communication-with-the-driver"></a>ドライバーとの通信を GDI


## <span id="ddk_gdi_communication_with_the_driver_gg"></span><span id="DDK_GDI_COMMUNICATION_WITH_THE_DRIVER_GG"></span>


ドライバーは、GDI に 1 つだけの関数をエクスポートします。[**DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210)します。 その他のドライバーでサポートされているなど、すべて機能、 [ **DrvDisableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556196)関数をポインターの配列を GDI に公開されます。 GDI の呼び出しを**DrvEnableDriver**ドライバーを初期化し、渡しますドライバーでサポートされているグラフィックのリスト DDI 関数。 一部の関数のドライバーをサポートする必要がありますが、GDI がドライバーから受信した関数の一覧に含まれていないこれらの操作を処理する**DrvEnableDriver**ルーチン。 GDI 呼び出し*DrvDisableDriver*ドライバーがロードする場合します。 詳細についてはグラフィックス DDI 関数[グラフィックス DDI を使用して](using-the-graphics-ddi.md)します。

GDI オブジェクトおよびサービスの数が多い使用できるようにドライバー。 これらが 2 つのカテゴリに分類されます。 ユーザー オブジェクトとサービス ルーチン。

 

 





