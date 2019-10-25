---
title: フィルター ドライバーの構成情報へのアクセス
description: フィルター ドライバーの構成情報へのアクセス
ms.assetid: 7d6bd7d4-3c06-4fc3-874b-fb8369ac227e
keywords:
- フィルタードライバーの WDK ネットワーク、構成情報
- NDIS フィルタードライバー WDK、構成情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d1106e45050ccd245964e5169151894b0104018
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835398"
---
# <a name="accessing-configuration-information-for-a-filter-driver"></a>フィルター ドライバーの構成情報へのアクセス





NDIS は、フィルタードライバーのレジストリパラメーターへのアクセスを提供する一連の関数をサポートしています。 フィルタードライバーは、アタッチまたは再起動操作中、またはプラグアンドプレイ (PnP) 通知を処理するときに、これらのパラメーターにアクセスできます。 PnP 通知の詳細については、「[フィルターモジュールの Pnp イベント通知](filter-module-pnp-event-notifications.md)」を参照してください。 フィルターモジュールのアタッチの詳細については、「[フィルターモジュールのアタッチ](attaching-a-filter-module.md)」を参照してください。 再起動操作の詳細については、「[フィルターモジュールを開始する](starting-a-filter-module.md)」を参照してください。

フィルタードライバーは、レジストリ設定にアクセスするために[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)関数を呼び出します。 フィルタードライバーが、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出して、 [**NDIS\_CONFIGURATION\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)構造の**NdisHandle**メンバー内のハンドルを取得した場合、 **NdisOpenConfigurationEx**関数フィルタードライバーの構成パラメーターが格納されているレジストリの場所のハンドルを提供します。 フィルタードライバーは、 [**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)関数を呼び出すまで、構成ハンドルを使用できます。

フィルタードライバーが[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数の*NdisFilterHandle*パラメーターから**NdisHandle**内のハンドルを取得した場合、 [**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)は、フィルターモジュールを使用するレジストリの場所へのハンドルを提供します。構成パラメーターが格納されます。 フィルタードライバーは、NDIS がフィルターモジュールをデタッチするまで構成ハンドルを使用でき、 [*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数はを返します。 監視フィルタドライバーが NDIS\_CONFIG\_フラグを指定している場合は、 [**ndis\_configuration\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_configuration_object)構造の**Flags**メンバー内の\_インスタンス\_構成フラグをフィルター処理\_ます。ドライバーは、同じミニポートアダプターに対して複数のフィルターモジュールが構成されている場合に、特定のフィルターモジュールのフィルターモジュール構成にアクセスできます。 フィルタードライバーを変更する場合は、このフラグを使用しないでください。

ドライバーが構成情報へのアクセスを完了した後、ドライバーは[**NdisCloseConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)関数を呼び出して、構成ハンドルと関連リソースを解放する必要があります。

 

 





