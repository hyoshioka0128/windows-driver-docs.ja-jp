---
title: フィルター ドライバーの構成情報へのアクセス
description: フィルター ドライバーの構成情報へのアクセス
ms.assetid: 7d6bd7d4-3c06-4fc3-874b-fb8369ac227e
keywords:
- フィルター ドライバー WDK ネットワー キング、構成情報
- NDIS フィルター ドライバー WDK、構成情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b470ab7d28d52803705d09bc53ba4a2582d027f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384431"
---
# <a name="accessing-configuration-information-for-a-filter-driver"></a>フィルター ドライバーの構成情報へのアクセス





NDIS は、フィルター ドライバーのレジストリ パラメーターへのアクセスを提供する関数のセットをサポートしています。 フィルター ドライバーでは、アタッチ中にこれらのパラメーターにアクセスしたり、操作またはプラグ アンド プレイ (PnP) 通知を処理するときに再起動することができます。 PnP 通知の詳細については、次を参照してください。[フィルター モジュールの PnP イベント通知](filter-module-pnp-event-notifications.md)します。 フィルター モジュールのインポートに関する詳細については、次を参照してください。[フィルター モジュールのアタッチ](attaching-a-filter-module.md)します。 再起動操作の詳細については、次を参照してください。[フィルター モジュールの開始](starting-a-filter-module.md)します。

ドライバーの呼び出しをフィルター処理、 [ **NdisOpenConfigurationEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)レジストリ設定にアクセスする関数。 フィルター ドライバーのハンドルを取得する場合、 **NdisHandle**のメンバー、 [ **NDIS\_構成\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_configuration_object)構造を呼び出すことによって、[ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数の場合、 **NdisOpenConfigurationEx**関数は、レジストリの場所を識別するハンドルを提供します場所フィルター。ドライバーの構成パラメーターが格納されます。 呼び出すまで、フィルター ドライバーは構成ハンドルを使用できます、 [ **NdisFDeregisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfderegisterfilterdriver)関数。

フィルター ドライバーのハンドルを取得する場合は**NdisHandle**から、 *NdisFilterHandle*のパラメーター、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数[ **NdisOpenConfigurationEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)フィルター モジュールの構成パラメーターを格納するレジストリの場所を識別するハンドルを提供します。 NDIS フィルター モジュールをデタッチするまで、フィルター ドライバーは構成のハンドルを使用できます、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数が返される。 監視するフィルター ドライバーは、NDIS を指定する場合\_CONFIG\_フラグ\_フィルター\_インスタンス\_の構成フラグ、**フラグ**のメンバー、 [**NDIS\_構成\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_configuration_object)構造体、ドライバー構成にアクセスできますフィルター モジュールを特定のフィルター モジュールの複数のフィルター モジュールがある場合にします。同じミニポート アダプタ上で構成されます。 フィルター ドライバーの変更では、このフラグは使用しないでください。

ドライバーが完了した後、ドライバーを呼び出す必要があります、構成情報にアクセスする、 [ **NdisCloseConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseconfiguration)構成ハンドルと関連リソースを解放する関数。

 

 





