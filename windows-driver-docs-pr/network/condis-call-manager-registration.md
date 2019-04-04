---
title: いる CoNDIS 呼び出すマネージャーの登録
description: いる CoNDIS 呼び出すマネージャーの登録
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- コール マネージャーの WDK ネットワー キング、いる CoNDIS
- 呼び出しのマネージャーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01ae1c677ac5d289a8fccd2bb10c03454b3c988e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557603"
---
# <a name="condis-call-manager-registration"></a>いる CoNDIS 呼び出すマネージャーの登録





スタンドアロンいる CoNDIS などその他のプロトコルのドライバー マネージャー、initialize を呼び出すしも追加いる CoNDIS エントリ ポイントを登録する必要があります。 プロトコル ドライバーの初期化の詳細については、[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)を参照してください。

いる CoNDIS エントリ ポイントを登録する*ProtocolXxx*関数呼び出しマネージャー呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)関数。 *ProtocolSetOptions*、いる CoNDIS プロトコルのすべてのドライバーが初期化、 [ **NDIS\_プロトコル\_CO\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566817)構造体し、渡すことで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーの初期化をコール マネージャーのエントリ ポイントを指定する、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)を構造化し、これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

ミニポート マネージャー (MCMs) も登録呼び出し manager 呼び出し*ProtocolXxx*関数。 MCM ドライバーの登録の詳細については、[いる CoNDIS MCM 登録](condis-mcm-registration.md)を参照してください。

省略可能なプロトコル ドライバー サービスを構成する方法の詳細については、[省略可能なプロトコル ドライバー サービスを構成する](configuring-optional-protocol-driver-services.md)を参照してください。

 

 





