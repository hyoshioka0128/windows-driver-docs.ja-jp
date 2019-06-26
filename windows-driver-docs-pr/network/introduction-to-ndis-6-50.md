---
title: NDIS 6.50 の概要
description: このセクションでは、NDIS 6.50 を紹介し、NDIS 6.40 からの変更について説明します。 Windows 10 バージョン 1507 以降では、NDIS 6.50 が含まれます。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e164df3212d946bad447722e838a4dd0a5e290
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386347"
---
# <a name="introduction-to-ndis-650"></a>NDIS 6.50 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.50 を示し、その主要な設計の追加機能を説明します。 Windows 10 バージョン 1507 以降では、NDIS 6.50 が含まれます。

NDIS 6.50 は、NDIS 6.40 にマイナー バージョン更新です。 NDIS 6.50 する NDIS 6.x ドライバーの移植の詳細については、次を参照してください。 [NDIS 6.50 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-50.md)します。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.50 NDIS 6.40 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-650-driver"></a>NDIS 6.50、ドライバーを実装します。

NDIS 6.50、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.50、ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.50、ドライバーは、NDIS に登録する際に正しい NDIS バージョンをレポートする必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.50 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーは 50 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[NDIS 6.50、ドライバーをコンパイルする](#compiling-an-ndis-650-driver))。

- Windows 10 用の NDIS 6.50 ミニポート ドライバー、バージョン 1507 以降は、データ構造の NDIS 6.50 バージョンを使用する必要があります。 詳細については、次を参照してください。[データ構造を使用する NDIS 6.50](#using-ndis-650-data-structures)します。

## <a name="compiling-an-ndis-650-driver"></a>NDIS 6.50、ドライバーのコンパイル

Windows 10 の WDK バージョン 1507 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.50 ドライバーがコンパイル時に適切な NDIS 6.50 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加```NDIS650_MINIPORT=1```します。
- フィルターまたはプロトコルのドライバーを追加```NDIS650=1```します。

Windows 10 バージョン 1507 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。

## <a name="using-ndis-650-data-structures"></a>NDIS 6.50 データ構造を使用

### <a name="new-data-structures"></a>新しいデータの構造

次のデータ構造は、NDIS 6.50 の新機能。

- [OID_WWAN_SYS_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)
- [OID_WWAN_DEVICE_CAPS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)
- [OID_WWAN_SLOT_INFO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)
- [OID_WWAN_NETWORK_IDLE_HINT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-network-idle-hint) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)
- [NDIS_PD_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_capabilities)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_close_provider_parameters)
- [NDIS_PD_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_config)
- [NDIS_PD_COUNTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_counter_parameters)
- [NDIS_PD_COUNTER_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_counter_value)
- [NDIS_PD_FILTER_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_filter_counter)
- [NDIS_PD_FILTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_filter_parameters)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_open_provider_parameters)
- [NDIS_PD_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_provider_dispatch)
- [NDIS_PD_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue)
- [NDIS_PD_QUEUE_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue_dispatch)
- [NDIS_PD_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue_parameters)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_receive_queue_counter)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_transmit_queue_counter)
- [PD_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer)
- [PD_BUFFER_8021Q_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer_8021q_info)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer_virtual_subnet_info)

### <a name="updated-data-structures"></a>更新されたデータ構造体

次のデータ構造は、NDIS 6.50 で更新されました。

- [NET_PNP_EVENT_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)
- [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)
- [NDIS_NET_BUFFER_LIST_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ne-ndis-_ndis_net_buffer_list_info)
- [NdisMGetDeviceProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetdeviceproperty)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_optional_handlers)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

## <a name="ndis-651"></a>NDIS 6.51

NDIS 6.51 は、NDIS 6.50 に非常にマイナー バージョン更新です。 Windows 10 バージョン 1511 以降では、NDIS 6.51 が含まれます。 NDIS 6.50 のすべての情報にも適用されます NDIS 6.51 次の例外。

- MinorNdisVersion は、50 から 51 NDIS ドライバーに登録するときに変更します。
- コンパイラ設定を変更```NDIS650_MINIPORT=1```ミニポート ドライバーと```NDIS650=1```フィルターまたはプロトコルのドライバーを```NDIS651_MINIPORT=1```と```NDIS651=1```それぞれ。

