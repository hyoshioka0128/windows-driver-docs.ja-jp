---
title: CoNDIS TAPI 登録
description: CoNDIS TAPI 登録
ms.assetid: 656be990-9392-4e8b-ac4a-73e38b75c109
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話 services WDK WAN、登録
- 接続 TAPI WDK ネットワーク、登録
- CoNDIS TAPI を登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a051edf66e6d3739c4963079ecfa4cb07e7b4f16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838185"
---
# <a name="condis-tapi-registration"></a>CoNDIS TAPI 登録





このセクションでは、CoNDIS WAN ミニポートドライバーによって、TAPI サービスがサポートされていること、および NDISWAN および NDPROXY ドライバーを使用して TAPI 固有の通信を設定する方法について説明します。

1つまたは複数の Nic に対して、2つのポートのミニポートドライバーのエントリポイントを登録した後、次の操作を行うと、NDISWAN および NDPROXY ドライバーが TAPI 固有の方法でこれらの Nic と関連付けられます。

-   CoNDIS WAN ミニポートドライバーは、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数内から[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)関数を呼び出して、呼び出しマネージャーエントリポイント、およびアドレスファミリタイプ CO\_ADDRESS\_ファミリ\_TAPI\_プロキシに登録します。 これにより、ミニポートドライバーは、TAPI サービスを提供することをアドバタイズします。

-   NDIS は、新しく登録されたアドレスファミリの NDPROXY に通知するために、NDPROXY の[**Protocolcoafregisternotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_af_register_notify)関数を呼び出します。 NDPROXY の*Protocolcoafregisternotify*は、アドレスファミリのデータを調べ、CONCOWAN ミニポートドライバーに統合されている通話マネージャーによって提供される TAPI サービスを使用できるかどうかを判断します。 TAPI 対応の WAN ミニポートドライバーは、統合されたミニポートコールマネージャー (MCM) ドライバーです。

-   NDPROXY は、NdisClOpenAddressFamilyEx 関数を呼び出して、 [**Condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex) WAN ミニポートドライバーに関連付けられている TAPI プロキシアドレスファミリを開きます。 **NdisClOpenAddressFamilyEx**は、ndproxy の接続指向エントリポイントを NDIS に登録します。 これらのエントリポイントは、TAPI 対応の接続 WAN ミニポートドライバーとの通信に使用されます。

-   NDPROXY は[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)を呼び出して、通話マネージャーのエントリポイント、およびアドレスファミリの種類 CO\_ADDRESS\_ファミリ\_TAPI に登録します。 これにより、NDPROXY は、TAPI サービスを実装することをアドバタイズします。

-   NDIS は、新しく登録されたアドレスファミリを NDISWAN に通知するために、NDISWAN の*Protocolcoafregisternotify*関数を呼び出します。 NDISWAN の*Protocolcoafregisternotify*は、アドレスファミリデータを調べ、NDISWAN が ndproxy によって提供される TAPI サービスを使用できることを判断します。

-   NDISWAN は、 **NdisClOpenAddressFamilyEx**関数を呼び出して、ndproxy に関連付けられている TAPI アドレスファミリを開きます。 **NdisClOpenAddressFamilyEx**は、NDISWAN の接続指向エントリポイントを NDIS に登録します。 これらのエントリポイントは、NDPROXY との通信に使用されます。

-   NDISWAN は、 [**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)関数を呼び出して、NDISWAN が特定のサービスアクセスポイント (SAP) の着信呼び出しを受け入れることができることを ndproxy に通知します。 この呼び出しで、NDISWAN は SAP を記述する[**CO\_sap**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))構造を渡します。 NDISWAN は、CO\_SAP の sap**型**メンバーを AF\_TAPI\_SAP\_TYPE に設定して、SAP が tapi 呼び出しに使用されることを指定します。 NDISWAN は、CO\_sap の**sap**メンバーを特定の TAPI デバイスクラスの文字列に設定します。 TAPI アプリケーションは、アプリケーションが TAPI **lineGetID**関数を呼び出すときにこの文字列を提供します。 NDPROXY は、SAP 宛てのすべての着信呼び出しについて NDISWAN に通知する必要があります。

 

 





