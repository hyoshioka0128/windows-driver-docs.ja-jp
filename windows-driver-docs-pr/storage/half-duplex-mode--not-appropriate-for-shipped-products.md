---
title: 半二重モードが適切で出荷された商品はありません。
description: 半二重モードが適切で出荷された商品はありません。
ms.assetid: a586f340-5577-40ba-aa3e-11599f506223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdacb9244eacd7a83b78cd8737732219cfc4c208
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378514"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>半二重モード: 出荷用製品には不適当


半二重モードのため、Storport ドライバー モデルに、SCSI ポート ドライバー モデルからミニポートの初期の移植時にのみ使用します。 ポート/ミニポート同期の実行を同期するロックが使用されている、SCSI ポート ミニポートの制限、 [ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)割り込みサービス ルーチンとします。 これによってデバイス IRQL (DIRQL) で時間をかけるになり、パフォーマンス低下につながる、処理、I/O の同時実行性を軽減します。 新しい Storport インターフェイスと最適化と互換性がありませんし、したがっては製品の出荷の使用は適していません。

半二重ミニポートを出荷する場合は、リスク Storport の将来のリビジョンで互換性の問題があります。

 

 




