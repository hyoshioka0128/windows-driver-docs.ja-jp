---
title: AGP サポート
description: AGP サポート
ms.assetid: 05a2f942-4374-421e-8292-d122f9fe3571
keywords:
- AGP WDK DirectDraw、AGP サポートについて
- 描画 AGP サポート WDK DirectDraw、AGP サポートについて
- DirectDraw AGP サポート AGP サポートについての WDK Windows 2000 の表示
- メモリ WDK DirectDraw AGP、AGP サポートについて
- 高速のグラフィックス ポート WDK DirectDraw
- メモリ WDK DirectDraw を表示します。
- WDK DirectDraw の非ローカルの表示メモリ
- メモリ WDK DirectDraw、AGP サポートの詳細を表示します。
- 非ローカルの表示メモリ WDK DirectDraw、非ローカルの表示メモリについて
- AGP WDK DirectDraw
- 描画 AGP サポート WDK DirectDraw
- DirectDraw AGP サポート WDK Windows 2000 の表示
- メモリ WDK DirectDraw AGP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b375f6a54598368728ca7a2ce15a5b64c2115b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539441"
---
# <a name="agp-support"></a>AGP サポート


## <span id="ddk_agp_support_gg"></span><span id="DDK_AGP_SUPPORT_GG"></span>


Microsoft DirectDraw 扱います*Accelerated グラフィックス ポート (AGP) メモリ*表示メモリのサブクラスとして。 このメモリの種類と呼びます*非ローカルの表示メモリ*します。 用語 AGP メモリと非表示のメモリは、DirectDraw と DirectDraw の観点から同義ドライバー。

AGP メモリは、表示のメモリの純粋なサブクラスと見なされます。 ドライバーでは、AGP メモリをサポートすることを示している場合ほとんどの場合が必要、ローカルと非表示のメモリの同じ機能が、パフォーマンスの違いが許可されているです。 例外は場合、DDCAPS2\_NONLOCALVIDMEMCAPS フラグが設定されて、表示のローカル メモリと異なる場合がこれを非ローカルの blt 機能がメモリを表示する場合。

たとえば、ドライバーの状態の表示メモリからテクスチャのことができる場合、できる必要がありますテクスチャを両方表示のローカルと非ローカル メモリから。 中は、同様に扱われます。 ドライバー、エクスポート色キーをソース blt 機能できることを元の色を行うには、blt をキーとしたとの間の非ローカルの表示メモリ。 このルールの 1 つの例外をから表示が非ローカル メモリに割り当てられたサーフェスの特定の種類を除外することはできます。 たとえば、ヒープをオーバーレイ サーフェスが AGP メモリに割り当てられたことを防ぐために使用することは。

AGP メモリは、表示のメモリのサブクラスとして扱われる、ため DirectDraw の AGP メモリのディスプレイ ドライバーのエントリ ポイントの別のセットがありません。 既存のディスプレイ ドライバーの呼び出しは、AGP サーフェスとローカルの表示メモリ サーフェスの両方に使用されます。 AGP と互換性のあるドライバーは、受信の表面を非ローカルまたはローカルの表示のメモリ内かどうかを確認し、適切な対処を必要があります。 AGP (その逆) システムから Blt ドライバー (この場合にする必要がありますサポート システム-AGP に転送も) システムに表示メモリ blt をサポートしていない限り、通常どおり DirectDraw エミュレーション層を経由します。

ドライバーは、DDCAPS2 を設定する必要があります\_TEXMANINNONLOCALVIDMEM フラグが可能な限り、Direct3D テクスチャ マネージャー AGP メモリ (システム メモリではなく) で、画面のビデオ メモリのコピーの場合は、そのバックアップ イメージを保持しているため、そう場合。

このセクションの残りの部分では、DirectDraw 非ローカルの表示メモリ機能を使用してサポート AGP メモリへの既存のドライバーを変更するために必要な手順について説明します。

 

 





