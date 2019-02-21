---
title: いる CoNDIS MCM の登録
description: いる CoNDIS MCM の登録
ms.assetid: 7dfb86c5-e7b6-4b9d-8f29-a6d247500c3e
keywords:
- MCMs WDK ネットワー キング、いる CoNDIS ミニポート コール マネージャーを登録します。
- ミニポート呼び出すマネージャー WDK ネットワー キング、いる CoNDIS ミニポート呼び出しを登録マネージャー
- ミニポート コール マネージャーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1de340cc58d057ccd4e426bc66f4921e869dd292
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550735"
---
# <a name="condis-mcm-registration"></a>いる CoNDIS MCM の登録





いる CoNDIS ミニポート コール マネージャー (MCMs) は、他のミニポート ドライバーのように初期化しも追加いる CoNDIS エントリ ポイントを登録する必要があります。 ミニポート ドライバーの初期化の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

いる CoNDIS エントリ ポイントを登録する*MiniportXxx*関数と*ProtocolXxx*関数、いる CoNDIS MCMs 呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。 *MiniportSetOptions*、MCM を初期化します、 [ **NDIS\_ミニポート\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565948)構造体を渡します*OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

MCMs の初期化呼び出し manager エントリ ポイントを登録する、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)構造体し、渡すことで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

省略可能なミニポート ドライバー サービスを構成する方法の詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

 

 





