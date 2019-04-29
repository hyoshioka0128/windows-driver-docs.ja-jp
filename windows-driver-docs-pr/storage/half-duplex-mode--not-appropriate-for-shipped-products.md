---
title: 半二重モードが適切で出荷された商品はありません。
description: 半二重モードが適切で出荷された商品はありません。
ms.assetid: a586f340-5577-40ba-aa3e-11599f506223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98e67329b967d4f5e2b17d0ead30cd677804e490
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390906"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>半二重モード: 出荷済み製品には不適


半二重モードのため、Storport ドライバー モデルに、SCSI ポート ドライバー モデルからミニポートの初期の移植時にのみ使用します。 ポート/ミニポート同期の実行を同期するロックが使用されている、SCSI ポート ミニポートの制限、 [ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)割り込みサービス ルーチンとします。 これによってデバイス IRQL (DIRQL) で時間をかけるになり、パフォーマンス低下につながる、処理、I/O の同時実行性を軽減します。 新しい Storport インターフェイスと最適化と互換性がありませんし、したがっては製品の出荷の使用は適していません。

半二重ミニポートを出荷する場合は、リスク Storport の将来のリビジョンで互換性の問題があります。

 

 




