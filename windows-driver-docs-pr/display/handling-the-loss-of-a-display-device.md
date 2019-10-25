---
title: ディスプレイデバイスの損失の処理
description: ディスプレイデバイスの損失の処理
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK ディスプレイ、デバイスの損失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4947937f8b2bc84bc6a58250086e3ac91c88db5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839657"
---
# <a name="handling-the-loss-of-a-display-device"></a>ディスプレイデバイスの損失の処理


次のシナリオでは、グラフィックスアダプターの出力コネクタでコンテンツ保護が有効になっている場合に、ディスプレイミニポートドライバーの[**DxgkDdiOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)関数の呼び出しが開始されます。

-   表示モードの変更

-   Windows デスクトップからのモニターの接続または切断

-   全画面表示のコマンドプロンプトウィンドウの入力

-   DirectDraw または Direct3D の排他モードアプリケーションの起動

-   ユーザーの簡易切り替えの実行

-   ワークステーションをロックするか、CTRL + ALT + DEL キーを押します。

-   リモートデスクトップ接続を使用したワークステーションへのアタッチ

-   省電力モードへの移行 (中断や休止など)

-   ページフォールトなどによってアプリケーションが予期せず終了する

 

 





