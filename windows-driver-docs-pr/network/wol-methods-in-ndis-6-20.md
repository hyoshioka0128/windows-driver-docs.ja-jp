---
title: NDIS 6.20 の WOL メソッド
description: NDIS 6.20 の WOL メソッド
ms.assetid: A46C213D-B356-44A3-8863-D7B183B73C77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c0566541438f701d7da58fb0ef642293e5ccf10
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385993"
---
# <a name="wol-methods-in-ndis-620"></a>NDIS 6.20 の WOL メソッド





NDIS 6.20 が動作し、以降のバージョンの NDIS でサポートされている電源管理機能は、次の wake on LAN (WOL) メソッドで構成されます。

-   Wake on マジック パケット

-   パターン マッチでスリープ解除します。

-   メディア上のウェイク アップのデバイスを接続します。

以前のバージョンの Windows 電源管理機能の詳細については、次を参照してください。 [(NDIS 6.0 以降) の電源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-20-)します。

*Wake on マジック パケット*メソッドは、ネットワーク アダプターが受信すると、コンピューターをウェイクする*マジック パケット*。 A*マジック パケット*受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーが含まれています。

*Wake on マジック パケット*メソッドとは別、*パターン マッチでスリープ解除*メソッド。 WOL パターンには、その他のパケットの種類またはビットマップが含まれます。 WOL パターンの詳細については、次を参照してください。 [NDIS 電源管理のパターンを WOL](wol-patterns-for-ndis-power-management.md)します。

一部のネットワーク アダプターのサポートを報告するが、*メディア ウェイク デバイス接続*メソッドでは、Windows の以前のバージョンではありませんでした。 Windows 7 を完全にサポート、*メディア ウェイク デバイス接続*メソッドの場合は、NDIS 6.20 ミニポート ドライバーのサポートを報告します。 NDIS は、メディアが切断された場合に、ネットワーク アダプターを低電力状態に設定します。

詳細については、*メディア ウェイク デバイス接続*メソッドを参照してください[メディア切断の低電力](low-power-on-media-disconnect.md)します。

 

 





