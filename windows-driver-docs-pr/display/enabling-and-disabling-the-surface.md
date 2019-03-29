---
title: サーフェスの有効化と無効化
description: サーフェスの有効化と無効化
ms.assetid: 34a1d1a5-b139-4d59-8754-b77d71bc75ad
keywords:
- 描画 WDK GDI、初期化を有効にして、画面を無効化
- 初期化のグラフィック ドライバー WDK Windows 2000 の表示を有効にして、画面を無効化
- GDI WDK Windows 2000 の表示、初期化を有効にして、画面を無効化
- グラフィック ドライバー WDK Windows 2000 を表示する初期化を有効にして、画面を無効化
- WDK GDI サーフェスの初期化
- WDK GDI を無効にする画面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47cda8256721daf09021a397865939f97ec2e11c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571408"
---
# <a name="enabling-and-disabling-the-surface"></a>サーフェスの有効化と無効化


## <span id="ddk_enabling_and_disabling_the_surface_gg"></span><span id="DDK_ENABLING_AND_DISABLING_THE_SURFACE_GG"></span>


GDI の呼び出しの最終初期化段階として**DrvEnableSurface**します。 *DrvEnableSurface*作成時に適切な GDI サービスを呼び出すことによって、画面の種類を指定する必要があります。 」の説明に従って[サーフェスの GDI サポート](gdi-support-for-surfaces.md)、デバイスと環境に応じて、ドライバーは、内から GDI の適切なサービスを呼び出すことが*DrvEnableSurface*サーフェスを作成します。

-   *画面のデバイスで管理された*、ドライバーを呼び出す必要があります、 [ **EngCreateDeviceSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564206)サーフェイスでのハンドルを取得する関数。

-   標準の形式を作成する (*DIB*) ビットマップの GDI 管理できることを完全には、すべての描画操作のパフォーマンスなど、ドライバーを呼び出す必要があります、 **EngCreateBitmap**ドライバー。

*DrvEnableSurface*戻り値として有効な表面のハンドルを返します。

次の画面の作成、ドライバー関連付ける必要がありますサーフェスを PDEV GDI サービスを呼び出して[ **EngAssociateSurface**](https://msdn.microsoft.com/library/windows/hardware/ff564183)します。 この呼び出しでは、GDI 描画する機能、ドライバーがそのサーフェイスでのフックについても説明します。

GDI の呼び出し、 [ **DrvDisableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556200)によって PDEV の現在の画面を作成したドライバーを通知する関数を*DrvEnableSurface*は必要なくなりました。 実行中に割り当てられているリソース、メモリ、ドライバーの割り当てを解除する必要があります*DrvEnableSurface*します。 *DrvDisableSurface*する前に必ず呼び出される[ **DrvDisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556198)PDEV を有効になっている画面がある場合、します。

作成されると、使用がの場合、画面を削除してください。 サーフェスの作成と削除を正しく一致するようにエラーには、無効なオブジェクトに蓄積し、システム パフォーマンスが低下する可能性があります。

 

 





