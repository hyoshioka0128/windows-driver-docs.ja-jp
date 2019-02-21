---
title: Vs の MCM ドライバー。コール マネージャー
description: Vs の MCM ドライバー。
ms.assetid: 374716fb-c192-42fd-bef0-0097d622f791
keywords:
- 接続指向 NDIS WDK、コール マネージャー
- いる CoNDIS WDK、ネットワー キング コール マネージャー
- 接続指向 NDIS WDK、MCM ドライバー
- いる CoNDIS WDK ネットワー キング、MCM ドライバー
- MCM ドライバー WDK ネットワーク
- マネージャーの WDK にネットワーク接続、vs を呼び出します。MCM ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88cb3a89aa64c58e67d4ef18ca2f8086a678ded
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532374"
---
# <a name="mcm-drivers-vs-call-managers"></a>Vs の MCM ドライバー。コール マネージャー





統合の MCM ドライバーは、クライアントの接続指向にもコール マネージャー サービスを提供する接続指向のミニポート ドライバーです。 そのため、MCM ドライバーの接続指向のミニポート ドライバーとコール マネージャーの両方のすべての接続指向関数を実行します。 すべてのミニポート ドライバーと同様に MCM のドライバーが使用する必要があります**Ndis * Xxx*** の呼び出しを基になる NIC ハードウェアと通信します。

MCM、ドライバーは、2 つの主要な方法でコール マネージャーとは異なります。

-   コール マネージャーは、接続指向、NDIS*プロトコル ドライバー*でコール マネージャーの機能を追加します。 MCM、ドライバーは接続指向、NDIS*ミニポート ドライバー*でコール マネージャーの機能を追加します。

-   NDIS--あるにコール マネージャーとの接続指向のミニポート ドライバー間のインターフェイスが公開されている完全、コール マネージャーとミニポート ドライバーの間のすべての通信は、NDIS を通過します。 を除き、アクティブ化と非アクティブ化クライアント (送信または受信のクライアント データを送信するために使用される VCs) VCs の MCM ドライバーのコール マネージャー部分と MCM ドライバーのミニポート ドライバー部分の間のインターフェイスは、NDIS に対して非透過的です。 アクティブ化とクライアントの VCs の非アクティブ化は、NDIS の追跡クライアント VCs のために、NDIS から実行する必要があります。

さらに、MCM ドライバーとコール マネージャーとの違いは、次のセクションで説明します。

[初期化の相違点](differences-in-initialization.md)

[NdisXxx 関数への呼び出しの違い](differences-in-calls-to-ndisxxx-functions.md)

[仮想接続の違い](differences-in-virtual-connections.md)

 

 





