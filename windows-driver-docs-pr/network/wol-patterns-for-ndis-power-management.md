---
title: NDIS 電源管理の WOL パターン
description: NDIS 電源管理の WOL パターン
ms.assetid: 44d49fe9-0983-4753-8f6f-f3445b5b9f3b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d769b7f8d0ca87df47368153100f015367a6a49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348620"
---
# <a name="wol-patterns-for-ndis-power-management"></a>NDIS 電源管理の WOL パターン





以降では、NDIS 6.20 が動作は、Wake on LAN (WOL) パターンは、*パターン マッチでスリープ解除*メソッド。 この WOL メソッドは、誤ったウェイク アップのイベントを最小化し、により、コンピューターに戻されました実行状態が予想される場合。 WOL パターンのインターフェイスは、パケットの種類 (たとえば、IPv4 で TCP SYN パケット) に基づく特定のパターンを識別します。 特定のパターンでは、信頼性の高いパターン一致を提供します。

WOL パターンの 2 種類あります。

<a href="" id="wol-packet-"></a>WOL パケット   
パケット、ウェイク アップ パターンが IPv4 で TCP SYN) などの特定のパケットの種類を定義します。

<a href="" id="wol-bitmap-"></a>WOL ビットマップ   
オフセットとビットマップを使用して指定されている WOL パターン。

**注**  NDIS 6.20 が動作し、以降のバージョンの NDIS もサポート、 *wake on マジック パケット*メソッド。 このメソッドは、*パターン マッチでスリープ解除*メソッド。

 

以降では、NDIS 6.20 が動作は、複数のプロトコル ドライバーは、ネットワーク アダプターを WOL パターンを設定できます。 WOL パターンの要求の数が、ネットワーク アダプターをサポートできる数より大きい場合に、正しい WOL パターンのセットが設定されていることを確認するには、プロトコル ドライバーは、WOL パターンごとに優先順位を割り当てます。 NDIS は、ネットワーク アダプターは、リソース不足になるため、新しい優先度の高い WOL パターンを追加することはできません、NDIS は低優先度のパターンを削除できます。

WOL パターンの管理に関する詳細については、次を参照してください。[の追加と削除 Wake on LAN パターン](adding-and-deleting-wake-on-lan-patterns.md)します。

NDIS 6.20 が動作し、以降のバージョンでサポートされる WOL メソッドの詳細については、次を参照してください。 [NDIS 6.20 WOL メソッド](introduction-to-ndis-6-20.md)します。

 

 





