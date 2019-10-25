---
title: ハーフデュプレックスモードは、出荷済み製品に適していません
description: ハーフデュプレックスモードは、出荷済み製品に適していません
ms.assetid: a586f340-5577-40ba-aa3e-11599f506223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072f1ba0bd9dd142e6a053bbce5070107c1768fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837559"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>半二重モード: 出荷済み製品に適していません


半二重モードは、SCSI ポートドライバーモデルから Storport ドライバーモデルにミニポートを最初に移植するときにのみ使用することを目的としています。 ポートとミニポートの同期は SCSI ポートミニポートのものに制限されます。ここでは、ロックを使用して、 [**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)および interrupt サービスルーチンの実行を同期します。 これにより、デバイスの IRQL (DIRQL) で時間が費やされ、i/o 処理の同時実行が減少し、パフォーマンスが低下します。 新しい Storport インターフェイスや最適化と互換性がないため、出荷製品での使用には適していません。

半二重のミニポートを出荷し続ける場合は、今後の Storport のリビジョンで互換性の問題が発生する可能性があります。

 

 




