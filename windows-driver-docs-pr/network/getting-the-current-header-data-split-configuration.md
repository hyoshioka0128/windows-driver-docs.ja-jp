---
title: 現在のヘッダー データの分割構成の取得
description: 現在のヘッダー データの分割構成の取得
ms.assetid: 62c5e362-4e19-465d-85a8-a8277cb46f5d
keywords:
- ヘッダー-データ分割 WDK、構成
- 現在のヘッダー-データ分割構成の WDK ネットワーク
- 状態情報 WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bcc91cbfae555f42b3c57186889fad58d8cf656
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842172"
---
# <a name="getting-the-current-header-data-split-configuration"></a>現在のヘッダー データの分割構成の取得





ミニポートアダプターの現在のヘッダーデータの分割設定を取得するために、それ以降のドライバーまたはユーザーモードアプリケーションは、[現在の\_CONFIG oid\_分割された\_GEN\_HD\_分割](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)できます。 ただし、それ以降のドライバーは、初期化中に NDIS によって提供される情報を使用し、状態を表示する必要があります。

システム管理者は、OID\_GEN\_HD\_分割された GUID を使用して、WMI インターフェイスを使用して現在の\_構成 OID を\_分割できます。 ヘッダーデータの分割 WMI Guid の詳細については、「 [wmi によるヘッダーデータの分割](wmi-support-for-header-data-split.md)」を参照してください。

NDIS は、ミニポートドライバーに代わって[現在の\_CONFIG\_分割\_\_HD\_GEN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)を処理します。 現在のヘッダーデータの分割構成情報は、ミニポートドライバーの初期化属性と[**ndis\_ステータス\_HD\_分割\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)の状態の表示に基づいて、ndis によって保持されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、[**現在の\_構成構造\_分割される ndis\_HD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)が含まれています。 また、NDIS は、初期化中に現在の\_CONFIG 構造\_分割され、状態が表示された状態で、NDIS\_HD\_分割します。

ミニポートドライバーが[\_GEN\_hd\_split\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) set request の分類を受け取ると、ドライバーは、 [**NDIS\_HD\_split\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)構造の内容を使用して現在のを更新する必要があります。ミニポートアダプターの構成。 更新後に、ミニポートドライバーは、 [**NDIS\_状態\_HD\_SPLIT\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状態の表示で変更を報告する必要があります。 状態の表示によって、すべてのドライバーが新しい情報で更新されます。

Ndis が NDIS 6.1 以降のプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis によって[ **\_パラメーター構造が\_バインド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)されます。これにより、NDIS [ **\_HD\_SPLIT\_現在の @no__ を指すことがt_11_ CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)構造体。

Ndis が NDIS 6.1 以降のフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出すと、ndis は NDIS\_フィルターを提供し、NDIS\_HD\_SPLIT\_現在の @no_ へのポインターを使用して[ **\_PARAMETERS 構造をアタッチ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)_t_10_ CONFIG 構造体。

 

 





