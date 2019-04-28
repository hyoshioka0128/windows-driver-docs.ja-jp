---
title: C28602
description: C28602 Sendmessagetimeout を HWND_BROADCAST を警告します。
ms.assetid: 511df04e-97dc-43a2-9c48-ea1ffe62b813
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28602
ms.openlocfilehash: a2f1f0411acf48ff50e4366b4145822019e686aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376774"
---
# <a name="c28602"></a>C28602


C28602 を警告します。Sendmessagetimeout HWND を\_ブロードキャスト

コード分析ツールは、アプリケーションを使用すると、この警告を報告**SendMessageTimeout**アプリケーション要求スレッドのタイムアウト期間を 10 秒のみの場合でも、します。 関数では、各ウィンドウがタイムアウトするまでは返されません。アプリケーションは、各ウィンドウが応答にかかる時間の長さの実際に禁止でした。 これは、他のすべての応答時間を制御することはできませんので**HWND**システムにします。

これを解決するには、使用を検討する**PostMessage**代わりに、そのためれていたブロック呼び出しです。 またの使用を回避する**HWND\_ブロードキャスト**特定のウィンドウにメッセージを送信します。

 

 





