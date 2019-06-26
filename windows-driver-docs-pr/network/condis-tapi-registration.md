---
title: CoNDIS TAPI 登録
description: CoNDIS TAPI 登録
ms.assetid: 656be990-9392-4e8b-ac4a-73e38b75c109
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- WDK WAN では、電話サービスを登録します。
- いる CoNDIS TAPI WDK ネットワーク、登録します。
- いる CoNDIS TAPI を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ddc8e5c51ad14564d892127dac7db5cca228c3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385101"
---
# <a name="condis-tapi-registration"></a>CoNDIS TAPI 登録





このセクションでは、いる CoNDIS WAN ミニポート ドライバーが TAPI サービスをサポートしていることを示す方法と、NDISWAN と NDPROXY ドライバーと TAPI に固有の通信を設定する方法について説明します。

いる CoNDIS WAN ミニポート ドライバーが 1 つまたは複数の Nic のミニポート ドライバー エントリ ポイントを登録した後、次の操作になるこれらの Nic を持つ、TAPI 固有の方法で、関連付けられている NDISWAN と NDPROXY ドライバーが発生します。

-   いる CoNDIS WAN ミニポート ドライバー呼び出し、 [ **NdisMCmRegisterAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex)関数内からその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数のコール マネージャーのエントリ ポイントと、アドレス ファミリの種類 CO を登録する\_アドレス\_ファミリ\_TAPI\_プロキシ。 これにより、ミニポート ドライバーは、TAPI サービスを提供することを通知します。

-   NDIS 呼び出し NDPROXY の[ **ProtocolCoAfRegisterNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_af_register_notify)に新しく登録されたアドレス ファミリの NDPROXY を通知する関数。 NDPROXY の*ProtocolCoAfRegisterNotify*アドレス ファミリのデータを調査している CoNDIS WAN ミニポート ドライバーに統合されているコール マネージャーによって提供される TAPI サービスを使用できることを決定します。 TAPI 対応いる CoNDIS WAN ミニポート ドライバーは、統合ミニポート コール マネージャー (MCM) ドライバーです。

-   NDPROXY 呼び出し、 [ **NdisClOpenAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclopenaddressfamilyex)いる CoNDIS WAN ミニポート ドライバーに関連付けられている TAPI プロキシ アドレス ファミリを開きます。 **NdisClOpenAddressFamilyEx** NDIS を NDPROXY の接続指向のエントリ ポイントを登録します。 これらのエントリ ポイントは、TAPI 対応いる CoNDIS WAN ミニポート ドライバーとの通信に使用されます。

-   NDPROXY 呼び出し[ **NdisCmRegisterAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)そのコール マネージャーのエントリ ポイントと、アドレス ファミリの種類 CO を登録する\_アドレス\_ファミリ\_TAPI します。 これにより、NDPROXY は TAPI サービスを実装することを通知します。

-   NDIS 呼び出し NDISWAN の*ProtocolCoAfRegisterNotify*に新しく登録されたアドレス ファミリの NDISWAN を通知する関数。 NDISWAN の*ProtocolCoAfRegisterNotify*アドレス ファミリのデータを調べ、NDISWAN NDPROXY によって提供される TAPI サービスを使用できることを決定します。

-   NDISWAN 呼び出し、 **NdisClOpenAddressFamilyEx** NDPROXY に関連付けられている TAPI アドレス ファミリを開きます。 **NdisClOpenAddressFamilyEx** NDIS を NDISWAN の接続指向のエントリ ポイントを登録します。 これらのエントリ ポイントは、NDPROXY との通信に使用されます。

-   NDISWAN 呼び出し、 [ **NdisClRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap) NDPROXY NDISWAN が着信呼び出しに特定サービス アクセス ポイント (SAP) を受け入れることを通知する関数。 この呼び出しで NDISWAN を渡します、 [ **CO\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85)) SAP を記述する構造体。 NDISWAN セット、 **SapType** CO のメンバー\_AF に SAP\_TAPI\_SAP\_TAPI 呼び出しのために、SAP が使用されることを指定する型。 NDISWAN セット、 **Sap** CO のメンバー\_SAP、特定の TAPI デバイス クラス用の文字列にします。 TAPI アプリケーションが、アプリケーションは、TAPI を呼び出すときに、この文字列を提供**lineGetID**関数。 NDPROXY は、SAP 宛てのすべての着信呼び出しについて NDISWAN を通知する必要があります。

 

 





