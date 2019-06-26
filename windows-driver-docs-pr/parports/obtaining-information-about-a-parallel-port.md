---
title: パラレル ポートに関する情報の取得
description: パラレル ポートに関する情報の取得
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- パラレル ポート WDK、情報を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dffbfd5980341de13063fd178f12b6affc456299
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358509"
---
# <a name="obtaining-information-about-a-parallel-port"></a>パラレル ポートに関する情報の取得





クライアントは、パラレル ポートを使用する前に、次の情報を取得できます。

-   パラレル ポートによって使用されるリソース

-   パラレル ポートのハードウェア機能

-   [パラレル ポート コールバック ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)カーネル モード ドライバーを使用します。

クライアントは、上記の情報を取得するのに次の内部デバイス制御要求を使用します。

[**IOCTL\_内部\_取得\_並列\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)

[**IOCTL\_内部\_取得\_詳細\_並列\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_more_parallel_port_info)

[**IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)

クライアントでは、パラレル ポート情報をリリースを使用して、 [ **IOCTL\_内部\_リリース\_並列\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_release_parallel_port_info)要求。

 

 




