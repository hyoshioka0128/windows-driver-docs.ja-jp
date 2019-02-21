---
title: ジェネリック識別子
description: ジェネリック識別子
ms.assetid: 75dab2fc-e897-4bce-b719-98ad89817fca
keywords:
- デバイスの識別文字列 WDK、ジェネリック
- 文字列の WDK デバイスを識別する、ジェネリック
- 識別子の WDK デバイス、ジェネリック
- 汎用デバイス識別子 WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd70bbbf262ee75cd713ff4651a07c6321cc8189
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537060"
---
# <a name="generic-identifiers"></a>ジェネリック識別子





識別子文字列のすべてではありませんが、そのほとんどは、bus 固有です。 プラグ アンド プレイ (PnP) マネージャーでは、多くの異なるバスに表示できるデバイスの汎用デバイス識別子のセットもサポートします。 これらの識別子は、フォームのことです。

\*PNPd(4)

d(4) は、4 桁の 16 進型識別子です。

PCMCIA バスの場合は、互換性 Id はこの方法で書式設定 (PCMCIA バスの次の説明を参照してください)。 これらの識別子の公式の一覧を検索する[プラグとベンダーの Id を再生し、デバイス Id](https://go.microsoft.com/fwlink/p/?linkid=49039) Microsoft ダウンロード センター。 参照してください[プラグ アンド プレイ ID - PNPID 要求](https://docs.microsoft.com/windows-hardware/drivers/install/plug-and-play-id---pnpid-request)詳細についてはします。 

 

 





