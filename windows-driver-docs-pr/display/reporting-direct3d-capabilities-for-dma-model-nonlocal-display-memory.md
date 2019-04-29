---
title: 非ローカルの表示メモリに対する Direct3D 機能のレポート
description: DMA モデルのドライバーでは、非ローカルの表示メモリ サーフェスの Direct3D 機能をエクスポートする必要があります。
ms.assetid: aa1b08c0-b212-48b6-a450-78d36951db80
keywords:
- DMA スタイル AGP WDK DirectDraw
- 表示メモリ WDK DirectDraw、DMA スタイル AGP
- 非ローカルの表示メモリ WDK DirectDraw、DMA スタイル AGP
- AGP WDK DirectDraw、DMA スタイル AGP
- 描画の AGP サポート WDK DirectDraw、DMA スタイル AGP
- DirectDraw AGP サポート DMA スタイル AGP、WDK の Windows 2000 の表示
- メモリ WDK DirectDraw AGP、DMA スタイル AGP
- Direct3D のレポート機能
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0b10858642009f8fd724675e786a09a82f968c83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383277"
---
# <a name="reporting-direct3d-capabilities-for-nonlocal-display-memory"></a>非ローカルの表示メモリに対する Direct3D 機能のレポート

DMA モデルのドライバーでは、非ローカルの表示メモリ サーフェスの Direct3D 機能もエクスポートする必要があります。 これは、レポートの DirectDraw 機能よりも大幅に簡略化します。 影響を受けた唯一の機能は、D3DDEVCAPS\_TEXTURENONLOCALVIDEOMEMORY します。 DMA モデルをエクスポートするディスプレイ カードは、非ローカルの表示メモリから直接テクスチャことができる場合、は、この機能を Direct3D デバイスの説明で設定があります。 できないと、アプリケーションを明示的に読み込む必要がありますまたは blt、非ローカル メモリ画面に表示ローカル メモリ画面テクスチャ リングを実行する前に、この機能は設定しないでください。 完全を期すため、execute の model ドライバーはこの機能のビットを常に設定する必要があります。

 

 





