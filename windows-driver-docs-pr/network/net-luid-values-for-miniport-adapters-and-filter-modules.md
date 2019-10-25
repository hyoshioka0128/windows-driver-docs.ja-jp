---
title: ミニポート アダプターとフィルター モジュールの NET_LUID 値
description: ミニポート アダプターとフィルター モジュールの NET_LUID 値
ms.assetid: d9135438-3399-4845-a28d-d445471cb41d
keywords:
- NDIS ネットワークインターフェイス WDK、NET_LUID
- ネットワークインターフェイス WDK、NET_LUID
- NET_LUID
- ミニポートアダプター WDK ネットワーク、NET_LUID 値
- フィルターモジュール WDK ネットワーク、NET_LUID 値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a78f97ef22bd710dfbc3beff83df4a5a1340481
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827235"
---
# <a name="net_luid-values-for-miniport-adapters-and-filter-modules"></a>ミニポートアダプターとフィルターモジュールの NET\_LUID 値





NDIS は、ミニポートドライバー (各ミニポートアダプター用) とフィルタードライバー (各フィルターモジュール用) に代わってインターフェイスを登録します。 プロトコルドライバーは、バインドハンドルを使用して、ドライバーがバインドされているミニポートアダプターのインターフェイスインデックスと[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値を NDIS に照会できます。 たとえば、MUX 中間ドライバーのプロトコルドライバーの下端が、内部インターフェイスの階層化順序を指定するために、NET\_LUID 値を取得する場合があります。

プロトコルドライバーは、 *NdisBindingHandle*パラメーターのバインドハンドルを[**NdisIfQueryBindingIfIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifquerybindingifindex)関数に渡し、フィルタースタックの最上位および下部にあるインターフェイスのインターフェイスインデックスと NET\_LUID 値を受け取ります。 また、プロトコルドライバーは、 [**NDIS\_バインド\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体でこれらの値を取得できます。

ミニポートドライバーは、NDIS ミニポートアダプターハンドルを使用して、ミニポートアダプターのインターフェイスインデックスを NDIS に照会することもできます。 ミニポートドライバーは、 [**NDIS\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体で、インターフェイスインデックスと NET\_LUID 値を受け取ります。

フィルタードライバーは、インターフェイスインデックスと NET\_LUID 値を取得します。このフィルターモジュールは、 [**NDIS\_フィルター\_ATTACH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体に含まれています。

 

 





