---
title: NDKPI 関数の実装
description: NDK 対応のミニポートドライバーは、すべての NDK_FN_XXX コールバック関数のエントリポイントを登録する必要があります。 NDKPI プロバイダーのコールバック関数はすべて必須です。none は省略可能です。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b92c918f5df6f5ec435d0e1f42ea057851cd39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833855"
---
# <a name="implementing-ndkpi-functions"></a>NDKPI 関数の実装


NDK 対応のミニポートドライバーは、すべての[ndk\_FN\_*XXX*コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)のエントリポイントを登録する必要があります。 NDKPI プロバイダーのコールバック関数はすべて必須です。none は省略可能です。

これらの関数のサポートを登録するために、ミニポートドライバーは、次の表の "オブジェクトのディスパッチテーブル" 列に示されている構造体にエントリポイントを格納します。

| オブジェクトの種類                                               | この関数によって作成された                                                                                                       | オブジェクトのディスパッチテーブル                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)                  | [ *\_NDK\_アダプター\_ハンドラーを開く*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)                                                             | [**NDK\_アダプター\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter_dispatch)                  |
| [**NDK\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)              | [*NDK\_FN\_\_コネクタの作成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_connector)                                                               | [**NDK\_コネクタ\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector_dispatch)              |
| [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)                            | [*NDK\_FN\_CREATE\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_cq)                                                                             | [**NDK\_CQ\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq_dispatch)                            |
| [**NDK\_リスナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)                | [*NDK\_FN\_\_リスナーの作成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_listener)                                                                 | [**NDK\_リスナー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener_dispatch)                |
| [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)                            | [*NDK\_FN\_作成\_MR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mr)                                                                             | [**NDK\_MR\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr_dispatch)                            |
| [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)                            | [*NDK\_FN\_作成\_MW*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mw)                                                                             | [**NDK\_MW\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw_dispatch)                            |
| [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)                            | [*NDK\_FN\_作成\_PD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_pd)                                                                             | [**NDK\_PD\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd_dispatch)                            |
| [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)                            | [*NDK\_fn\_\_qp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp)または[ *NDK\_fn\_\_qp\_を作成*\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq)   | [**NDK\_QP\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp_dispatch)                            |
| [**NDK\_共有\_エンドポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint) | [*NDK\_FN\_\_共有\_エンドポイントの作成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_shared_endpoint)                                                  | [**NDK\_共有\_エンドポイント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint_dispatch) |
| [**NDK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)                          | [*Ndk\_fn\_\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_srq) [*の\_fn\_\_QP\_を*作成\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq) | [**NDK\_\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq_dispatch)                          |

 

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






