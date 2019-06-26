---
title: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
description: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
ms.assetid: 1a3ac1b1-9180-4b71-8740-70c6fbe9a885
keywords:
- IEEE 1284 WDK
- パラレル ポート WDK、IEEE 1284 デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b461a9a30a53bb1fb6be264a94f397d9c2ad461
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358486"
---
# <a name="selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-port"></a>パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除





クライアントは、選択し、次の内部デバイス制御要求を使用してパラレル ポートに接続されている、IEEE 1284.3 デバイスの選択を解除します。

[**IOCTL\_内部\_選択\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_select_device)

[**IOCTL\_内部\_解除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_deselect_device)

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を使用して取得される、 [ **IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)要求。 この要求を返します、 [**並列\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parallel_pnp_information)システム提供のコールバックに次のポインターを含む構造体。

-   **TrySelectDevice**メンバーへのポインターを[ *PPARALLEL\_を再試行してください\_選択\_日常的な*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_try_select_routine)コールバックで、選択を解除します。IEEE 1284.3 デイジー チェーン デバイスまたはパラレル ポートに接続されている IEEE 1284 チェーンの最後のデバイス。

-   **DeselectDevice**メンバーへのポインターを[ *PPARALLEL\_解除\_ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_deselect_routine)コールバックを IEEE 1284.3 デイジー チェーンを選択します。デバイスまたはパラレル ポートに接続されている IEEE 1284 チェーンの最後のデバイス。

の要求が最も低いパラレル ポートが別のクライアントが割り当てられている場合、パラレル ポートのシステムによって提供される関数のドライバーがクライアントの選択の要求をキューにあるため、クライアントによって処理します。 パラレル ポート関数ドライバーには、要求がキューから後、は、IEEE 1284.3 デバイスを選択して、ポートを割り当てることを試行します。 クライアントは、タイムアウトの許容遅延またはその他デバイス固有の条件のため、いつでも選択の要求をキャンセルできます。

**注**  クライアントのみを使用する場合、 [ **PPARALLEL\_を再試行してください\_選択\_日常的な**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_try_select_routine)並列を選択しようとするコールバックデバイス、およびその他のクライアントをパラレル ポートの競合しているシステムによって提供される関数のドライバーをパラレル ポート可能性があることはありません、ポートに割り当てるクライアント。 成功を確実には、クライアントを使用する必要があります、 [ **IOCTL\_内部\_選択\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_select_device)要求。 (パラレル ポート関数ドライバーのキュー、およびその後プロセス、ポートの要求の割り当てし、デバイスが選択するデバイスで要求が受信した順序で要求を選択します)。

 

パラレル ポート機能のドライバーを選択すると、クライアントに対して IEEE 1284.3 デバイスをクライアントが、ポートと、選択した IEEE 1284.3 デバイスへの排他アクセスします。 クライアントが呼び出す必要があります、 [ **PPARALLEL\_解除\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_deselect_routine)ポートを解放して、IEEE 1284.3 デバイスの選択を解除するコールバック。 クライアントが、ポートを解放した後、パラレル ポート関数ドライバーが存在する場合は、保留中の要求をキューからし、要求を処理します。

Microsoft Windows 2000 は、ポートごとに 4 つデイジー チェーン接続デバイスをサポートしています。ただし、ポートごとに最大で 2 つのデイジー チェーン接続デバイスの使用をお勧めします。 Windows XP では、1 ポートあたり最大で 2 つデイジー チェーンのデバイスをサポートします。

 

 




