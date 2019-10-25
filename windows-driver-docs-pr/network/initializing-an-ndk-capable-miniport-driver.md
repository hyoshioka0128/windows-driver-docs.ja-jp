---
title: NDK 対応ミニポート ドライバーの初期化
description: ネットワークダイレクトカーネル (NDK) をサポートするミニポートドライバーは、他のミニポートドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリポイントも登録する必要があります。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2d265e369276bf66a50d560e08ab028f5b9627
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824486"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>NDK 対応ミニポート ドライバーの初期化


ネットワークダイレクトカーネル (NDK) をサポートするミニポートドライバーは、他のミニポートドライバーと同じ方法で初期化されます。 ただし、追加の NDKPI エントリポイントも登録する必要があります。

-   [DriverEntry 関数](#driverentry-function)
-   [MiniportSetOptions 関数](#miniportsetoptions-function)
-   [関連トピック](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 関数


すべてのミニポートドライバーの[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数は、次のページで説明されているように、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造を初期化し、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)に渡します。

-   [ミニポートドライバーの初期化](initializing-a-miniport-driver.md)
-   [**NDIS ミニポートドライバー関数の DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)

NDK 対応ミニポートドライバーは、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造を初期化するときに、次の操作を行う必要があります。

-   **OidRequestHandler**メンバーでは、ミニポートドライバーは次の機能をサポートする[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を登録する必要があります。

    -   すべての[Ndkpi oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

    -   一般に NDIS ミニポートドライバーに必須の Oid。

        **注**  必須の oid の一覧については、「[ミニポートドライバーの必須の oid](https://docs.microsoft.com/windows-hardware/drivers/network/mandatory-oids-for-miniport-drivers)」を参照してください。

         

-   **SetOptionsHandler**メンバーでは、「[オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)」と「次の MiniportSetOptions 関数」の説明に従って、ミニポートドライバーが[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を登録する必要があります。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 関数


NDIS は、ミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)関数から制御が戻った直後に、 [*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出します。 *MiniportSetOptions*関数は、ミニポートドライバーの[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)呼び出しのコンテキストで呼び出されます。

この[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数では、ndk 対応のミニポートドライバーにより、ndk 機能が登録され、次の必要な ndkpi 関数のエントリポイントが登録されます[(オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)に関するページを参照してください)。

-   *Openndkadapterhandler* ([*OPEN\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler))

-   *Closendkadapterhandler* ([ *\_NDK\_アダプター\_ハンドラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-close_ndk_adapter_handler))

これらの関数の NDKPI エントリポイントを登録するには、ミニポートドライバーの[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数で次の操作を行う必要があります。

1.  [**NDIS\_NDK\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)の構造体を初期化します。

    **注**  は、**ヘッダー**メンバーの説明に特に注意を払ってください。 ミニポートドライバーは、それ自体を NDK 対応ミニポートドライバーとして識別するように、このメンバーを正しく設定する必要があります。

     

2.  関数のエントリポイントを、構造体の**Openndkadapterhandler**および**closendkadapterhandler**メンバーに格納します。

3.  [**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出して、パラメーターを指定した*ハンドラー*パラメーターで構造体を渡します。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






