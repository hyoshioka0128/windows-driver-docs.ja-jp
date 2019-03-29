---
title: CoNDIS クライアント登録
description: CoNDIS クライアント登録
ms.assetid: 335dd117-f6c8-4416-8527-ff64c1a5f3ee
keywords:
- クライアント登録 WDK いる CoNDIS
- エントリ ポイントを登録します。
- WDK のネットワー キングのエントリ ポイントします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 418c5bd919bca2119c933d4629888deb7bed0bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573630"
---
# <a name="condis-client-registration"></a>CoNDIS クライアント登録





いる CoNDIS クライアントは、その他のプロトコル ドライバーなどを初期化しも追加いる CoNDIS エントリ ポイントを登録する必要があります。 プロトコル ドライバーの初期化の詳細については、次を参照してください。[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)します。

いる CoNDIS エントリ ポイントを登録する*ProtocolXxx*関数、いる CoNDIS クライアントの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)関数。 *ProtocolSetOptions*、いる CoNDIS プロトコルのすべてのドライバーが初期化、 [ **NDIS\_プロトコル\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566817)構造体し、渡すことで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーの初期化をいる CoNDIS クライアントのエントリ ポイントを指定する、 [ **NDIS\_CO\_クライアント\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564884)構造体これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

省略可能なプロトコル ドライバー サービスを構成する方法の詳細については、次を参照してください。[省略可能なプロトコル ドライバー サービスを構成する](configuring-optional-protocol-driver-services.md)します。

 

 





