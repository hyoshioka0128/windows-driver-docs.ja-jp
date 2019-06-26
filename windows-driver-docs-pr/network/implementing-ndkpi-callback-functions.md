---
title: NDKPI 関数の実装
description: NDK 対応のミニポート ドライバーでは、すべて NDK_FN_XXX コールバック関数のエントリ ポイントを登録する必要があります。 NDKPI プロバイダーのコールバック関数のすべてが必須です。[なし] は省略可能です。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b8a4b52c54dcd2e211190d9f454eb307687e91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374855"
---
# <a name="implementing-ndkpi-functions"></a>NDKPI 関数の実装


NDK 対応のミニポート ドライバーは、すべてのエントリ ポイントを登録する必要があります[NDK\_FN\_*XXX*コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。 NDKPI プロバイダーのコールバック関数のすべてが必須です。[なし] は省略可能です。

これらの関数のサポートを登録するには、ミニポート ドライバーでは、「オブジェクトのディスパッチ テーブル」のデータ構造で、エントリ ポイントを格納、次の表の列。

| オブジェクトの種類                                               | この関数によって作成されました。                                                                                                       | オブジェクトのディスパッチ テーブル                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_ADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)                  | [*OPEN\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler)                                                             | [**NDK\_ADAPTER\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter_dispatch)                  |
| [**NDK\_CONNECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)              | [*NDK\_FN\_CREATE\_CONNECTOR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_connector)                                                               | [**NDK\_コネクタ\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector_dispatch)              |
| [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq)                            | [*NDK\_FN\_CREATE\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_cq)                                                                             | [**NDK\_CQ\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq_dispatch)                            |
| [**NDK\_LISTENER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener)                | [*NDK\_FN\_CREATE\_LISTENER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_listener)                                                                 | [**NDK\_リスナー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener_dispatch)                |
| [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr)                            | [*NDK\_FN\_CREATE\_MR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_mr)                                                                             | [**NDK\_MR\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr_dispatch)                            |
| [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw)                            | [*NDK\_FN\_CREATE\_MW*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_mw)                                                                             | [**NDK\_MW\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw_dispatch)                            |
| [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd)                            | [*NDK\_FN\_CREATE\_PD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_pd)                                                                             | [**NDK\_PD\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd_dispatch)                            |
| [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)                            | [*NDK\_FN\_作成\_QP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp)または[ *NDK\_FN\_作成\_QP\_WITH\_手順*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq)   | [**NDK\_QP\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp_dispatch)                            |
| [**NDK\_SHARED\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint) | [*NDK\_FN\_作成\_SHARED\_エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_shared_endpoint)                                                  | [**NDK\_SHARED\_エンドポイント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint_dispatch) |
| [**NDK\_SRQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)                          | [*NDK\_FN\_作成\_の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_srq)または[ *NDK\_FN\_作成\_QP\_WITH\_手順*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq) | [**NDK\_SRQ\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq_dispatch)                          |

 

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






