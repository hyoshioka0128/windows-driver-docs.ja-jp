---
title: 非表示のメモリに対するレポート機能は DDraw
description: DMA モデルのドライバーでは、ローカルの表示メモリよりもメモリを非表示の別の機能があります。
ms.assetid: e503fc8b-db27-486a-8616-a1b88ea77218
keywords:
- DMA スタイル AGP WDK DirectDraw
- 表示メモリ WDK DirectDraw、DMA スタイル AGP
- 非ローカルの表示メモリ WDK DirectDraw、DMA スタイル AGP
- AGP WDK DirectDraw、DMA スタイル AGP
- 描画の AGP サポート WDK DirectDraw、DMA スタイル AGP
- DirectDraw AGP サポート DMA スタイル AGP、WDK の Windows 2000 の表示
- メモリ WDK DirectDraw AGP、DMA スタイル AGP
- レポートの DirectDraw 機能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 92475ad722fdf15ade9ae5c8fd09382db2f5ecf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383274"
---
# <a name="reporting-directdraw-capabilities-for-nonlocal-display-memory"></a>非ローカルの表示メモリに対する DirectDraw 機能のレポート

DMA モデルのドライバーでは、ローカルの表示メモリよりもメモリを非表示の別の機能があります。 たとえば、ディスプレイ カードが blit ローカル メモリいますが、表示しない非ローカル メモリ サーフェスを拡張することがあります。 場合、ドライバー、DDCAPS2\_サーフェイスに表示が非ローカル メモリの DirectDraw 機能の NONLOCALVIDMEMCAPS フラグ、ドライバーが検出された、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)ドライバーエントリ ポイントです。 このプローブを識別する GUID が GUID\_NonLocalVidMemCaps します。

DirectDraw のこのリリースでは、ドライバーのみ機能を指定して blt の非ローカルの表示メモリから表示のローカル メモリに注意してください。 転送表示の非ローカル メモリにローカルの表示メモリと非表示のメモリを非表示のメモリからは、DirectDraw HEL によって常にエミュレートされます。 この制限は、将来のリリースで緩和される可能性があります。

 

 





