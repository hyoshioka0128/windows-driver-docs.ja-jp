---
title: NDIS 6.30 データ構造の使用
description: NDIS 6.30 データ構造の使用
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a27846a7057cccc2510b9428cefae14c463b07d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842983"
---
# <a name="using-ndis-630-data-structures"></a>NDIS 6.30 データ構造の使用


NDIS では、同じデータ構造の複数のバージョンをサポートできます。 Windows 8 および Windows Server 2012 オペレーティングシステムでは、構造体の NDIS 6.30 バージョンを使用するミニポートドライバーは、正しいバージョンとサイズの値を使用して、構造体の**ヘッダー**メンバーを初期化する必要があります。 **ヘッダー**メンバーは、ヘッダー構造[ **\_の ndis\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)であり、ドライバーは、**ヘッダー**メンバーの**リビジョン**メンバーと**サイズ**メンバー値を ndis 6.30 バージョンとサイズ値に初期化する必要があります。

**注**  正しいバージョンとサイズの情報を確認するには、**ヘッダー**メンバーを含む各構造の参照ページを参照してください。 **ヘッダー**メンバーを含み、ndis 6.30 用に更新された構造体の参照ページには、ndis 6.30 ドライバーの新しい情報が含まれています。 NDIS 6.30 の構造が更新されていない場合は、以前のバージョンの NDIS 用に提供されている情報が NDIS 6.30 ドライバーにも適用されます。

 

NDIS 6.30 では、次の構造が更新されました。

- [**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)
- [**NDIS\_ミニポート\_アダプターの\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)
- [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
- [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)
- [**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))
- [**NDIS\_NET\_BUFFER\_LIST\_フィルター処理\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)
- [**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle)
- [**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)
- [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)
- [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)
- [**NDIS\_受信\_フィルター\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)
- [**NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)
- [**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)
- [**NDIS\_RECEIVE\_QUEUE\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)
- [**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)
- [**NDIS\_受信\_スケール\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)
- [**NDIS\_RSS\_プロセッサ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)
- [**NDIS\_共有\_メモリ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)
 

 





