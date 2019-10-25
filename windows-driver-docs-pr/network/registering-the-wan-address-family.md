---
title: WAN アドレス ファミリの登録
description: WAN アドレス ファミリの登録
ms.assetid: 31443e99-24d8-4276-8345-004b0eeb05d7
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、TAPI アドレスファミリ
- NdisCmRegisterAddressFamilyEx
- TAPI WDK ネットワーク
- WAN アドレスファミリを登録しています
- WAN アドレスファミリの WDK ネットワーク
- アドレスファミリ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51473ebe69e5fc23e0fda4e3ccac3da5afd58321
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842066"
---
# <a name="registering-the-wan-address-family"></a>WAN アドレス ファミリの登録





このトピックでは、CoNDIS WAN ミニポートコールマネージャー (MCM) または別の呼び出しマネージャーから TAPI アドレスファミリを登録する方法について説明します。

どちらの種類の呼び出しマネージャーも、 [**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)関数を呼び出して呼び出しマネージャーエントリポイントを登録し、アドレスファミリの種類 CO\_ADDRESS\_ファミリ\_TAPI\_プロキシに登録します。 これにより、ドライバーは TAPI サービスを提供していることを示します。 CoNDIS ドライバーでのアドレスファミリの登録の詳細については、「[アドレスファミリの登録とオープン](registering-and-opening-an-address-family.md)」を参照してください。

NDIS は、新しく登録されたアドレスファミリの NDPROXY に通知します。 NDPROXY は、コールマネージャーによって提供される TAPI サービスを使用できることを判断します。 NDPROXY は、ドライバーに関連付けられている TAPI プロキシアドレスファミリを開き、NDPROXY の接続指向エントリポイントを NDIS に登録します。 これらのエントリポイントは、ドライバーとの通信に使用されます。

NDPROXY はミニポートドライバーの TAPI 機能を列挙し、後で NDIS 構造にカプセル化されている TAPI 要求を送信できます。 TAPI サポートでの CoNDIS 拡張機能の使用の詳細については、「 [Condis Services をサポートする WAN 操作](condis-wan-operations-that-support-telephonic-services.md)」を参照してください。

 

 





