---
title: NDIS 6.50 の概要
description: このセクションでは、NDIS 6.50 について説明し、NDIS 6.40 からの変更について説明します。 NDIS 6.50 は、Windows 10 バージョン1507以降に含まれています。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0370193a95eb2d9ef19da8005114e50f09999779
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844169"
---
# <a name="introduction-to-ndis-650"></a>NDIS 6.50 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.50 について説明し、主な設計の追加について説明します。 NDIS 6.50 は、Windows 10 バージョン1507以降に含まれています。

NDIS 6.50 は、NDIS 6.40 に対するマイナーバージョンの更新です。 Ndis 6. x ドライバーを ndis 6.50 に移植する方法の詳細については、「ndis [6. x ドライバーを ndis 6.50 に移植する](porting-ndis-6-x-drivers-to-ndis-6-50.md)」を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.50 は NDIS 6.40 の増分更新であり、主要な新機能は含まれていません。

## <a name="implementing-an-ndis-650-driver"></a>NDIS 6.50 ドライバーの実装

NDIS 6.50 ドライバーは、「 [ndis 6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で定義されている要件に従う必要があります。

また、NDIS 6.50 ドライバーは、次の要件に準拠している必要があります。

- Ndis 6.50 ドライバーは、ndis に登録するときに正しい NDIS バージョンを報告する必要があります。
   
   NDIS 6.50 をサポートするには、NDIS_Xxx_DRIVER_CHARACTERISTICS 構造体のメジャーおよびマイナーバージョン番号を更新する必要があります。 MajorNdisVersion メンバーには6を含める必要があり、MinorNdisVersion メンバーには50が含まれている必要があります。 この要件は、ミニポート、プロトコル、およびフィルタードライバーに適用されます。 また、コンパイラのバージョン情報も更新する必要があります (「 [NDIS 6.50 ドライバーのコンパイル](#compiling-an-ndis-650-driver)」を参照してください)。

- Windows 10 バージョン1507以降の NDIS 6.50 ミニポートドライバーでは、データ構造の NDIS 6.50 バージョンを使用する必要があります。 詳細については、「 [NDIS 6.50 データ構造体の使用](#using-ndis-650-data-structures)」を参照してください。

## <a name="compiling-an-ndis-650-driver"></a>NDIS 6.50 ドライバーのコンパイル

Windows 10 バージョン1507の WDK は、ヘッダーのバージョン管理をサポートしています。 ヘッダーのバージョン管理により、コンパイル時に NDIS 6.50 ドライバーが適切な NDIS 6.50 データ構造を使用するようになります。

次のコンパイラ設定をドライバーの Visual Studio プロジェクトに追加します。

- ミニポートドライバーの場合は、```NDIS650_MINIPORT=1```を追加します。
- フィルターまたはプロトコルドライバーの場合は、```NDIS650=1```を追加します。

Windows 10 バージョン1507リリースの WDK を使用したドライバーの構築の詳細については、「[ドライバーのビルド](../develop/building-a-driver.md)」を参照してください。

## <a name="using-ndis-650-data-structures"></a>NDIS 6.50 データ構造体の使用

### <a name="new-data-structures"></a>新しいデータ構造

次のデータ構造は、NDIS 6.50 で新しく追加されたものです。

- [OID_WWAN_SYS_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)
- [OID_WWAN_DEVICE_CAPS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)
- [OID_WWAN_SLOT_INFO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)
- [OID_WWAN_NETWORK_IDLE_HINT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-network-idle-hint) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)
- [NDIS_PD_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_capabilities)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_close_provider_parameters)
- [NDIS_PD_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)
- [NDIS_PD_COUNTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_counter_parameters)
- [NDIS_PD_COUNTER_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_counter_value)
- [NDIS_PD_FILTER_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_filter_counter)
- [NDIS_PD_FILTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_filter_parameters)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)
- [NDIS_PD_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_provider_dispatch)
- [NDIS_PD_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue)
- [NDIS_PD_QUEUE_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue_dispatch)
- [NDIS_PD_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue_parameters)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_receive_queue_counter)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_transmit_queue_counter)
- [PD_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer)
- [PD_BUFFER_8021Q_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer_8021q_info)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer_virtual_subnet_info)

### <a name="updated-data-structures"></a>更新されたデータ構造

次のデータ構造は、NDIS 6.50 で更新されました。

- [NET_PNP_EVENT_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)
- [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)
- [NDIS_NET_BUFFER_LIST_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_net_buffer_list_info)
- [NdisMGetDeviceProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_optional_handlers)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

## <a name="ndis-651"></a>NDIS 6.51

NDIS 6.51 は、NDIS 6.50 に対する非常にマイナーバージョンの更新です。 NDIS 6.51 は、Windows 10 バージョン1511以降に含まれています。 NDIS 6.50 のすべての情報は、次の例外を除き、NDIS 6.51 にも適用されます。

- MinorNdisVersion は、ドライバーを NDIS に登録するときに50から51に変更されます。
- コンパイラの設定は、ミニポートドライバーの場合は ```NDIS650_MINIPORT=1``` から、フィルターまたはプロトコルドライバーの場合は ```NDIS650=1``` に、それぞれ ```NDIS651_MINIPORT=1``` および ```NDIS651=1``` に変更されます。

