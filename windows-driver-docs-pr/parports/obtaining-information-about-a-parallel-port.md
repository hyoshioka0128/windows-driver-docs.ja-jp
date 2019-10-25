---
title: パラレル ポートに関する情報の取得
description: パラレル ポートに関する情報の取得
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- パラレルポート WDK、情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b762df9f899e1a1d47670d35dbb043cce9f1762f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844497"
---
# <a name="obtaining-information-about-a-parallel-port"></a>パラレル ポートに関する情報の取得





クライアントがパラレルポートを使用する前に、次の情報を取得できます。

-   パラレルポートで使用されるリソース

-   パラレルポートのハードウェア機能

-   カーネルモードドライバーが使用できる[パラレルポートコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

クライアントは、次の内部デバイス制御要求を使用して、上記の情報を取得します。

[**IOCTL\_内部\_\_並列\_ポート\_情報を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)

[**IOCTL\_内部\_\_\_並列\_ポート\_情報を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_more_parallel_port_info)

[**IOCTL\_内部\_\_パラレル\_PNP\_情報を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)

クライアントは、 [**IOCTL\_内部\_リリース\_並列\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_release_parallel_port_info)要求を使用して、パラレルポート情報を解放します。

 

 




