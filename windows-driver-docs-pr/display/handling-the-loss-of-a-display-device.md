---
title: ディスプレイ デバイスの喪失の処理
description: ディスプレイ デバイスの喪失の処理
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK ディスプレイ、デバイスの紛失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f2122928103ca266e6f1df63dfcf770824f87b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369838"
---
# <a name="handling-the-loss-of-a-display-device"></a>ディスプレイ デバイスの喪失の処理


次のシナリオは、表示のミニポート ドライバーに呼び出しを開始する[ **DxgkDdiOPMDestroyProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)グラフィックス アダプターのコンテンツの保護のコネクタがありますの出力中に関数有効になります。

-   表示モードの変更

-   アタッチまたはデタッチ Windows デスクトップからの監視

-   全画面表示のコマンド プロンプト ウィンドウを入力します。

-   任意の DirectDraw または Direct3D 排他モード アプリケーションの開始

-   ユーザーの簡易切り替えを実行します。

-   ワークステーションをロックまたは CTRL + ALT + DEL キーを押します

-   リモート デスクトップ接続を使用して、ワークステーションへのアタッチ

-   たとえば、中断または休止状態に省電力モードの場合--

-   アプリケーション予期せずに終了 - たとえば、ページ フォールトを

 

 





