---
title: NDIS 6.30 データ構造の使用
description: NDIS 6.30 データ構造の使用
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2edb9c85534851bca190c3a3ef935b780261c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371799"
---
# <a name="using-ndis-630-data-structures"></a>NDIS 6.30 データ構造の使用


NDIS は、同じデータ構造体の複数のバージョンをサポートできます。 Windows 8 および Windows Server 2012 オペレーティング システムで、構造体の NDIS 6.30 バージョンを使用するミニポート ドライバーを初期化する必要があります、**ヘッダー**適切なバージョンとサイズの値構造体のメンバー。 **ヘッダー**メンバーは、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)構造、およびドライバーを初期化する必要があります、**リビジョン**メンバーと**サイズ**のメンバーの値、**ヘッダー** NDIS 6.30 バージョン、およびサイズをメンバー。

**注**  適切なバージョンおよびサイズの情報を含む各構造のリファレンス ページを参照してください。 を決定する、**ヘッダー**メンバー。 含む構造体のリファレンス ページを**ヘッダー** NDIS 6.30 には、NDIS 6.30 ドライバーの新しい情報が含まれているメンバーとするが更新されました。 NDIS 6.30 の構造体への更新プログラムがない場合は、以前のバージョンの NDIS 提供される情報は、NDIS 6.30 ドライバーにも当てはまります。

 

NDIS 6.30 の次の構造が更新されました。

- [**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)
- [**NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)
- [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
- [**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)
- [**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))
- [**NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)
- [**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [**NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_offload_handle)
- [**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)
- [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)
- [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)
- [**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)
- [**NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)
- [**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)
- [**NDIS\_受信\_キュー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)
- [**NDIS\_受信\_キュー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)
- [**NDIS\_受信\_スケール\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)
- [**NDIS\_RSS\_プロセッサ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)
- [**NDIS\_SHARED\_メモリ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_shared_memory_parameters)
 

 





