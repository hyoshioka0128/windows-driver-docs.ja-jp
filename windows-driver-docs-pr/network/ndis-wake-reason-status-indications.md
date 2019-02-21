---
title: NDIS ウェイク理由状態インジケーター
description: NDIS ウェイク理由状態インジケーター
ms.assetid: 0229A4F3-8CC1-4A81-9AF4-33BAEBDAE954
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bd5322b1dd532d20f4cc1dca6fa8120c157b2a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552248"
---
# <a name="ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態インジケーター


NDIS 6.30 以降、ミニポート ドライバーで NDIS ウェイク アップの理由の状態を示す値を発行 ([**NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) するNDIS とシステムのウェイク アップ イベントの理由についての上にあるドライバーに通知します。 ネットワーク アダプターでは、ウェイク アップのイベントを生成する場合、ミニポート ドライバーはシステムの電力状態に再開時この NDIS 状態を示す値を発行するすぐにします。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

ここでは、次のトピックについて説明します。

[NDIS ウェイク理由状態インジケーターの概要](overview-of-ndis-wake-reason-statue-indications.md)

[レポートのウェイク アップの理由の状態を示す値機能](reporting-wake-reason-status-indication-capabilities.md)

[発行元の NDIS ウェイク理由状態インジケーター](issuing-ndis-wake-reason-indications.md)

 

 





