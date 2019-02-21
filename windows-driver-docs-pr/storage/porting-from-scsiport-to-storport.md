---
title: ScsiPort から StorPort への移植
description: ScsiPort から StorPort への移植
ms.assetid: 2a14051d-dc23-4420-a3e5-0827b16b1e42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b4868d662d747d964e662280dff9be86aaea6e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538336"
---
# <a name="porting-from-scsiport-to-storport"></a>ScsiPort から StorPort への移植


Storport ベース ミニポート ドライバーに Scsiport ベース ミニポート ドライバーからのサンプル コードを移植するために必要なれた移植活動の概要を次に示します。

-   NextRequest と NextLuRequest のすべての呼び出しを削除します

-   すべての ScsiPortXxx StorPortXxx 呼び出しの名前を変更します。

-   BuildIo ルーチンの追加 (移動 StartIo からコードの約 75%)

-   ドライバーを全二重操作に変換します。

-   キュー管理ルーチン (エラー処理、アダプターの再起動) を追加します。

-   LUN とターゲットのリセットのサポートを追加します。

-   内部的にキューのタグを割り当てるコードを追加 (ハードウェアの制限)

-   バスのリセットとアダプターの完全な再起動用の同期ルーチンを追加します。

-   SRB のサポートを追加\_関数\_POWER (アダプター SRB をシャット ダウン)

-   StorPortSetDeviceQueueDepth 呼び出し--LUN キューの深さが 31 日に設定を追加します。

 

 




