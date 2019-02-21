---
title: アドレス ファミリ
description: アドレス ファミリ
ms.assetid: d40df44e-f88b-4181-84ab-3fbf37172aaf
keywords:
- 接続指向 NDIS WDK、アドレス ファミリ
- いる CoNDIS の WDK は、ネットワーク アドレス ファミリ
- アドレス ファミリの WDK ネットワーク
- AFs WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3e1360239b5d10ac36e01e8b069ff713cdc36a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560325"
---
# <a name="address-families"></a>アドレス ファミリ





*アドレス ファミリ*(AF) は、次のドライバーのいずれかの間のアソシエーションを表します。

-   接続指向のクライアント、コール マネージャー、および基になる接続指向のミニポート ドライバー。

-   接続指向のクライアントと特定のシグナリング プロトコルの MCM ドライバー。

アドレス ファミリには、特定の信号プロトコルも指定します。

コール マネージャーまたは MCM ドライバーは、NDIS を使用して、アドレス ファミリを登録することによって特定のシグナリング プロトコルに対してその呼び出しマネージャー サービスをアドバタイズします。 NDIS は、新しく登録されたアドレス ファミリのバインディングで各クライアントを通知します。 コール マネージャーまたは MCM ドライバーによって提供されるコール マネージャー サービスを使用できる、前に、接続指向のクライアントは、コール マネージャーやアドバタイズ MCM ドライバーのアドレス ファミリを開く必要があります。

アドレス ファミリでの操作についての詳細については、次を参照してください。[を登録すると、アドレス ファミリを開く](registering-and-opening-an-address-family.md)と[アドレス ファミリを閉じる](closing-an-address-family.md)します。

 

 





