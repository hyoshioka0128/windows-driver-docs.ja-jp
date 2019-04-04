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
ms.openlocfilehash: ba250c892ae3cdecc4f5918adf294fc3ae116720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581323"
---
# <a name="quality-of-service"></a>サービスの品質 (QoS)





SVC に対する呼び出しの発信元を指定できます*サービスの品質*呼び出しの呼び出しのパフォーマンス パラメーターを指定する (QoS) パラメーター。 シグナリング プロトコルによって使用されている、コール マネージャーまたはである、発信または着信呼び出しを設定している MCM ドライバーは、ネットワーク スイッチなど、リモート クライアントのネットワーク エンティティの QoS をネゴシエートできます。 シグナリングのプロトコルによって許可されている場合は、着信呼び出しを受け入れるかどうかを決定するときに、接続指向のクライアントも QoS の変更を要求可能性があります。

呼び出しの QoS パラメーターが呼び出しのパラメーターとして指定された、 [ **CO\_呼び出す\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545384)構造体。 CO\_呼び出す\_パラメーターが指す他の 2 つの構造。

-   [**CO\_呼び出す\_MANAGER\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff545381)を指定するマネージャーのパラメーターを呼び出すコール マネージャーまたは MCM ドライバーを使用して呼び出しを設定します。

-   [**CO\_メディア\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff545388)、メディア パラメーターを指定するが、ミニポート ドライバーまたは MCM ドライバーの VC をアクティブ化に使用します。

両方の共同\_呼び出す\_MANAGER\_パラメーターと CO\_メディア\_パラメーター、パラメーターを使用するすべてのドライバーに適用されるジェネリック パラメーター (フラグ) に含まれます。 各構造体も指す、 [ **CO\_特定\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff545396)コール マネージャー固有のパラメーターを指定する構造体 (COを指すとき\_呼び出す\_MANAGER\_パラメーター構造体) またはメディア固有のパラメーター (CO によって示されるときに\_メディア\_パラメーター構造体)。

QoS の操作の詳細については、[Client-Initiated を呼び出すパラメーターの変更を要求](client-initiated-request-to-change-call-parameters.md)と[呼び出しパラメーターの変更を受信した要求](incoming-request-to-change-call-parameters.md)を参照してください。

 

 





