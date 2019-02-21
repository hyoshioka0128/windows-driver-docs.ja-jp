---
title: デバイスの LSI_U3 サンプル Storport ミニポート ドライバー
description: デバイスの LSI_U3 サンプル Storport ミニポート ドライバー
ms.assetid: 1ac63d07-f85c-492b-9886-f40a19d7c0b2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a76fd738869e78f5aad6e72a55b0fb000dcd68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529032"
---
# <a name="sample-storport-miniport-driver-for-an-lsiu3-device"></a>サンプル Storport ミニポート ドライバー、LSI の\_U3 デバイス


LSI\_WDK に含まれている U3 Storport ミニポート ドライバー サンプル コードは、LSI の実稼働 SYM\_U3 Scsiport ベース ミニポート ドライバーが Storport Scsiport ではなく操作に移植されるからです。 結果として得られるベースの Storport ミニポート ドライバー サポート LSI Ultra160 並列 SCSI ホスト バス アダプターを 53 C 1010 33 または 53 C 1010 66 チップです。 これらのホスト バス アダプターの特性のいくつか挙げます。

-   古いテクノロジ最小限のインテリジェンスで SCSI コント ローラーのハードウェア

-   8 KB の内部 RAM を備えた非常に単純なカスタムの 8 ビット RISC プロセッサ

-   ハードウェアとアダプターごとのキュー タグ値の 256 を使用する制限のスクリプト

-   ハードウェアとスクリプト Scsiport 機能に一致するように設計されています

LSI の調整が行われた\_Storport に合わせて U3 ミニポート ドライバー拡張機能ホストのハードウェアに限り機能するバス アダプター自体。

 

 




