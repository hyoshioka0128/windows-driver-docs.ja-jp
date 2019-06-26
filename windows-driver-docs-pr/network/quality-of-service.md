---
title: サービスの品質 (QoS)
description: サービスの品質 (QoS)
ms.assetid: e7a4413c-633b-4634-a647-c84b8c97cbea
keywords:
- 接続指向 NDIS WDK、サービスの品質
- ネットワーク接続、サービスの品質いる CoNDIS WDK
- WDK いる CoNDIS サービスの品質
- QoS WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0672b71557012165da225615585df93f61ff4d61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385451"
---
# <a name="quality-of-service"></a>サービスの品質 (QoS)





SVC に対する呼び出しの発信元を指定できます*サービスの品質*呼び出しの呼び出しのパフォーマンス パラメーターを指定する (QoS) パラメーター。 シグナリング プロトコルによって使用されている、コール マネージャーまたはである、発信または着信呼び出しを設定している MCM ドライバーは、ネットワーク スイッチなど、リモート クライアントのネットワーク エンティティの QoS をネゴシエートできます。 シグナリングのプロトコルによって許可されている場合は、着信呼び出しを受け入れるかどうかを決定するときに、接続指向のクライアントも QoS の変更を要求可能性があります。

呼び出しの QoS パラメーターが呼び出しのパラメーターとして指定された、 [ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体。 CO\_呼び出す\_パラメーターが指す他の 2 つの構造。

-   [**CO\_呼び出す\_MANAGER\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))を指定するマネージャーのパラメーターを呼び出すコール マネージャーまたは MCM ドライバーを使用して呼び出しを設定します。

-   [**CO\_メディア\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))、メディア パラメーターを指定するが、ミニポート ドライバーまたは MCM ドライバーの VC をアクティブ化に使用します。

両方の共同\_呼び出す\_MANAGER\_パラメーターと CO\_メディア\_パラメーター、パラメーターを使用するすべてのドライバーに適用されるジェネリック パラメーター (フラグ) に含まれます。 各構造体も指す、 [ **CO\_特定\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))コール マネージャー固有のパラメーターを指定する構造体 (COを指すとき\_呼び出す\_MANAGER\_パラメーター構造体) またはメディア固有のパラメーター (CO によって示されるときに\_メディア\_パラメーター構造体)。

QoS の操作の詳細については、次を参照してください。 [Client-Initiated を呼び出すパラメーターの変更を要求](client-initiated-request-to-change-call-parameters.md)と[呼び出しパラメーターの変更を受信した要求](incoming-request-to-change-call-parameters.md)します。

 

 





