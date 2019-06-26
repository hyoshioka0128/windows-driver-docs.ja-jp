---
title: NDK 対応ミニポート ドライバーの初期化
description: Network Direct カーネル (NDK) をサポートしているミニポート ドライバーは、その他のミニポート ドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリ ポイントまた登録する必要があります。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28600f6afabb6831224844423262b71baa6c098
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381292"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>NDK 対応ミニポート ドライバーの初期化


Network Direct カーネル (NDK) をサポートしているミニポート ドライバーは、その他のミニポート ドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリ ポイントまた登録する必要があります。

-   [DriverEntry 関数](#driverentry-function)
-   [MiniportSetOptions 関数](#miniportsetoptions-function)
-   [関連トピック](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 関数


すべてのミニポート ドライバーの[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数を初期化します、 [ **NDIS\_ミニポート\_ドライバー\_特性** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体し、それを[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)ように、次のページで説明されています。

-   [ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)
-   [**NDIS ミニポート ドライバーの DriverEntry 関数**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)

初期化するときに、NDK 対応のミニポート ドライバーは、次を実行する必要があります、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体。

-   **OidRequestHandler**メンバー、ミニポート ドライバーを登録する必要があります、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)をサポートする関数。

    -   すべて[NDKPI Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)します。

    -   必須の NDIS ミニポート ドライバーは、一般の Oid。

        **注**  これらの必須の Oid の一覧は、次を参照してください。[ミニポート ドライバーに必須の Oid](https://docs.microsoft.com/windows-hardware/drivers/network/mandatory-oids-for-miniport-drivers)します。

         

-   **SetOptionsHandler**メンバー、ミニポート ドライバーを登録する必要があります、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)で説明されているとおりに機能[オプションを構成します。ミニポート ドライバー サービス](configuring-optional-miniport-driver-services.md)と次の MiniportSetOptions 関数セクション。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 関数


NDIS 呼び出し、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数、ミニポート ドライバーの後すぐに[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数が返される。 *MiniportSetOptions*ミニポート ドライバーの呼び出しのコンテキストで関数を呼び出す[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。

その[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数、NDK 対応のミニポート ドライバーは、次の必要な NDKPI 関数のエントリ ポイント」の説明に従って、NDK 機能とレジスタを登録[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md):

-   *OpenNDKAdapterHandler* ([*オープン\_NDK\_アダプター\_ハンドラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler))

-   *CloseNDKAdapterHandler* ([*CLOSE\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-close_ndk_adapter_handler))

NDKPI エントリを登録するポイント、これらの関数、ミニポート ドライバーの[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数は、次を実行する必要があります。

1.  初期化を[ **NDIS\_NDK\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)構造体。

    **注**  に特に注意してください、**ヘッダー**メンバーの説明。 ミニポート ドライバーでは、NDK 対応のミニポート ドライバーとして自身を識別するために、このメンバーを正しく設定する必要があります。

     

2.  関数のエントリ ポイントを格納、 **OpenNDKAdapterHandler**と**CloseNDKAdapterHandler**構造体のメンバー。

3.  呼び出す、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)で構造体を引数として関数を*OptionalHandlers*パラメーター。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






