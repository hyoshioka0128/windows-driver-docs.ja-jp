---
title: アドレス ファミリ
description: アドレス ファミリ
ms.assetid: d40df44e-f88b-4181-84ab-3fbf37172aaf
keywords:
- 接続指向 NDIS WDK、アドレスファミリ
- CoNDIS WDK ネットワーク、アドレスファミリ
- アドレスファミリ WDK ネットワーク
- AFs WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3e1360239b5d10ac36e01e8b069ff713cdc36a6
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750015"
---
# <a name="address-families"></a>アドレス ファミリ





*アドレスファミリ*(AF) は、次のいずれかのドライバーセット間の関連付けを表します。

-   接続指向クライアント、コールマネージャー、および基になる接続指向ミニポートドライバー。

-   接続指向クライアントと、特定のシグナリングプロトコル用の MCM ドライバー。

アドレスファミリは、特定のシグナリングプロトコルも指定します。

呼び出しマネージャーまたは MCM ドライバーは、アドレスファミリを NDIS に登録することによって、特定のシグナリングプロトコルの呼び出しマネージャーサービスをアドバタイズします。 その後、NDIS は、新しく登録されたアドレスファミリのバインドで各クライアントに通知します。 呼び出しマネージャーまたは MCM ドライバーによって提供される call manager サービスを使用するには、接続指向クライアントが、そのアドレスファミリを提供した call manager または MCM ドライバーで開く必要があります。

アドレスファミリに対する操作の詳細については、「[アドレスファミリの登録とオープン](registering-and-opening-an-address-family.md)」および「[アドレスファミリの終了](closing-an-address-family.md)」を参照してください。

 

 





