---
title: DirectX ランタイムの動作
description: DirectX ランタイムの動作
ms.assetid: 98cfb09c-74ed-4329-b663-5f813a84debe
keywords:
- DirectX のランタイム回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 372583ec4dba115e3a086f43a8d259ecc442cca0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327936"
---
# <a name="directx-runtime-behavior"></a>DirectX ランタイムの動作


Microsoft DirectX のランタイムのさまざまなバージョンでは、ドライバーの代わりに次の回転状況を処理します。

-   Microsoft DirectDraw ランタイムでは、ディスプレイを回転したときにオーバーレイを表示しようとすると自動的に失敗します。

-   DirectX のランタイムのすべてのバージョンでは、スキャン ラインの値は、解像度の高さの最大範囲全体をカバーするため、プライマリの画面の回転中に返されるスキャン ラインの値を調整します。 それ以外の場合、ビームを追跡しようとするアプリケーションが画面の幅よりも大きいスキャン ライン値の待機しているかどうかと、アプリケーションがそれ以外の場合ことはありませんが、縦モードで応答を停止する可能性があります。

-   DirectX のランタイムのすべてのバージョンでは、エミュレーションのさまざまなフォームを使用するウィンドウ表示モードのデバイスで行われた、回転のプライマリ画面へのすべてのアクセスを処理します。

 

 





