---
title: NDIS 6.20 WOL メソッド
description: NDIS 6.20 WOL メソッド
ms.assetid: A46C213D-B356-44A3-8863-D7B183B73C77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8cd7dc9eb916b4ba5aaa10e816e7fd7616954f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530602"
---
# <a name="wol-methods-in-ndis-620"></a>NDIS 6.20 WOL メソッド





NDIS 6.20 が動作し、以降のバージョンの NDIS でサポートされている電源管理機能は、次の wake on LAN (WOL) メソッドで構成されます。

-   Wake on マジック パケット

-   パターン マッチでスリープ解除します。

-   メディア上のウェイク アップのデバイスを接続します。

以前のバージョンの Windows 電源管理機能の詳細については、[(NDIS 6.0 以降) の電源管理](https://msdn.microsoft.com/library/windows/hardware/hh205401)を参照してください。

*Wake on マジック パケット*メソッドは、ネットワーク アダプターが受信すると、コンピューターをウェイクする*マジック パケット*。 A*マジック パケット*受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーが含まれています。

*Wake on マジック パケット*メソッドとは別、*パターン マッチでスリープ解除*メソッド。 WOL パターンには、その他のパケットの種類またはビットマップが含まれます。 WOL パターンの詳細については、[NDIS 電源管理のパターンを WOL](wol-patterns-for-ndis-power-management.md)を参照してください。

一部のネットワーク アダプターのサポートを報告するが、*メディア ウェイク デバイス接続*メソッドでは、Windows の以前のバージョンではありませんでした。 Windows 7 を完全にサポート、*メディア ウェイク デバイス接続*メソッドの場合は、NDIS 6.20 ミニポート ドライバーのサポートを報告します。 NDIS は、メディアが切断された場合に、ネットワーク アダプターを低電力状態に設定します。

詳細については、*メディア ウェイク デバイス接続*メソッドを参照してください[メディア切断の低電力](low-power-on-media-disconnect.md)します。

 

 





