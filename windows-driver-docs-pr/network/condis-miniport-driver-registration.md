---
title: CoNDIS ミニポート ドライバー登録
description: CoNDIS ミニポート ドライバー登録
ms.assetid: 2dfd3bdc-b7b1-4491-b05e-2e8e1f5895b8
keywords:
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS ミニポート ドライバー WDK、いる CoNDIS
- ミニポート ドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a46119f695d7abd76fb5fb16c119263adc40f24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367676"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS ミニポート ドライバー登録





いる CoNDIS ミニポート ドライバーでは、その他のミニポート ドライバーのように初期化しも追加いる CoNDIS エントリ ポイントを登録する必要があります。 ミニポート ドライバーの初期化の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

いる CoNDIS エントリ ポイントを登録する*MiniportXxx*関数、いる CoNDIS ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[*MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。 *MiniportSetOptions*、ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565948)構造体を渡しますで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

ミニポート register を呼び出すマネージャー (MCMs) も*ProtocolXxx*関数*MiniportSetOptions*します。 MCM ドライバーの登録の詳細については、次を参照してください。[いる CoNDIS MCM 登録](condis-mcm-registration.md)します。

省略可能なミニポート ドライバー サービスを構成する方法の詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

 

 





