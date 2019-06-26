---
title: 現在のヘッダー データの分割構成の取得
description: 現在のヘッダー データの分割構成の取得
ms.assetid: 62c5e362-4e19-465d-85a8-a8277cb46f5d
keywords:
- ヘッダー データの分割 WDK、構成
- 現在のヘッダー データの分割 WDK ネットワークの構成
- ステータス情報 WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447fda131cd2c3049420a689da23be01de1002cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382752"
---
# <a name="getting-the-current-header-data-split-configuration"></a>現在のヘッダー データの分割構成の取得





現在を取得するヘッダー データが重なってドライバー、ミニポート アダプターの設定を分割したり、ユーザー モード アプリケーションを照会できます、 [OID\_GEN\_HD\_分割\_現在\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config) OID。 ただし、ドライバーを後続の初期化中に、状態インジケーターの NDIS に提供する情報を使用する必要があります。

システム管理者が、OID に関連付けられている GUID を使用できます\_GEN\_HD\_分割\_現在\_WMI インターフェイスから OID を構成します。 ヘッダー データの詳細については、WMI の Guid を分割するを参照してください。[ヘッダー データの分割のサポートを WMI](wmi-support-for-header-data-split.md)します。

NDIS ハンドル[OID\_GEN\_HD\_分割\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)ミニポート ドライバーの代わりです。 NDIS に現在のヘッダー データの分割、ミニポート ドライバーと初期化の属性に基づく構成情報は、および[ **NDIS\_状態\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状態を示す値。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)構造体。 NDIS は、NDIS も用意されています。\_HD\_分割\_現在\_状態の表示と初期化中にドライバーを関連する構造体を構成します。

ミニポート ドライバーが受信すると、 [OID\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)セットの要求、ドライバーの内容を使用する必要があります、 [ **NDIS\_HD\_分割\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)ミニポート アダプターの現在の構成を更新する構造体。 ミニポート ドライバーの更新後での変更を報告する必要があります、 [ **NDIS\_状態\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状態を示す値。 状態の表示により、新しい情報ですべての上にあるドライバーが更新されるようになります。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex) NDIS 6.1 またはそれ以降のプロトコル ドライバー、NDIS の関数を提供する[ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)へのポインターを含む構造体、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)構造体。

NDIS を呼び出すと、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach) NDIS 6.1 またはそれ以降のフィルター ドライバー、NDIS の関数を提供する[ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters) 、NDIS へのポインターを使用した構造\_HD\_分割\_現在\_構成構造体。

 

 





