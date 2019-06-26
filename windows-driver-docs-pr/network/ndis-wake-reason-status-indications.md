---
title: NDIS ウェイク理由状態表示
description: NDIS ウェイク理由状態表示
ms.assetid: 0229A4F3-8CC1-4A81-9AF4-33BAEBDAE954
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cc620edd24dcd9a7b9ec3311293eb5d8204d473
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386227"
---
# <a name="ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示


NDIS 6.30 以降、ミニポート ドライバーで NDIS ウェイク アップの理由の状態を示す値を発行 ([**NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) するNDIS とシステムのウェイク アップ イベントの理由についての上にあるドライバーに通知します。 ネットワーク アダプターでは、ウェイク アップのイベントを生成する場合、ミニポート ドライバーはシステムの電力状態に再開時この NDIS 状態を示す値を発行するすぐにします。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

ここでは、次のトピックについて説明します。

[NDIS ウェイク理由状態インジケーターの概要](overview-of-ndis-wake-reason-statue-indications.md)

[レポートのウェイク アップの理由の状態を示す値機能](reporting-wake-reason-status-indication-capabilities.md)

[発行元の NDIS ウェイク理由状態インジケーター](issuing-ndis-wake-reason-indications.md)

 

 





