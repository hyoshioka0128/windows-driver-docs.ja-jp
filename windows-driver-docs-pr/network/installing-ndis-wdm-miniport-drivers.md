---
title: NDIS-WDM ミニポート ドライバーのインストール
description: NDIS-WDM ミニポート ドライバーのインストール
ms.assetid: 7b87d8e3-cefa-49d7-ae66-0c3d771e24ef
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワーク, インストール
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、ドライバーのインストール
- WDM 低い edge WDK ネットワー キング、ドライバーのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a757161240a7ab057329c16392cad5fb71e3f3b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324890"
---
# <a name="installing-ndis-wdm-miniport-drivers"></a>NDIS-WDM ミニポート ドライバーのインストール





NDIS WDM のミニポート ドライバーのインストール メカニズムを実装するときに注意してください、次のものをおく必要があります。

-   情報 (INF) ファイルを作成、 **Net** 」の説明に従って、ネットワーク コンポーネントのクラス[ネットワーク INF ファイルの作成](creating-network-inf-files.md)です。

-   いずれかの通常行われるように、デバイスのプラグ アンド プレイ (PnP) 識別子 (ID) を含める**Net** ; のネットワーク コンポーネントのクラスただし、これらの Id に固有の作成、デバイスが接続されているバスの種類。

 

 





