---
title: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
description: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
ms.assetid: 1a3ac1b1-9180-4b71-8740-70c6fbe9a885
keywords:
- IEEE 1284 WDK
- パラレルポート WDK、IEEE 1284 デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126866337ab2f7c159b27ad68a273242f36dd779
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842324"
---
# <a name="selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-port"></a>パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除





クライアントは、次の内部デバイス制御要求を使用して、パラレルポートに接続されている IEEE 1284.3 デバイスを選択および選択解除できます。

[**IOCTL\_内部\_\_デバイスの選択**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_select_device)

[**IOCTL\_内部\_\_デバイスの選択を解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_deselect_device)

カーネルモードドライバーでは、システムによって提供される[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用することもできます。これは、 [**IOCTL\_内部\_\_パラレル\_PNP\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)要求を使用して取得されます。 この要求は、システムによって提供されるコールバックへの次のポインターを含む、[**パラレル\_PNP\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_pnp_information)構造体を返します。

-   **Tryselectdevice**メンバーは、 [*pparallel\_\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_select_routine)を指すポインターです。\_ルーチンコールバックを選択します。これにより、パラレルポートに接続されている ieee 1284.3 デイジーチェーンデバイスまたは ieee 1284 末端チェーンデバイスが選択解除されます。

-   **Deselectdevice**メンバーは、 [*PPARALLEL\_選択解除\_ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_deselect_routine)コールバックへのポインターであり、パラレルポートに接続されている ieee 1284.3 デイジーチェーンデバイスまたは ieee 1284 末端チェーンデバイスを選択します。

パラレルポートが別のクライアントによって割り当てられている場合は、並列ポート用のシステム提供の関数ドライバーによってクライアントの select 要求がキューに配置されるため、select 要求はクライアントによる処理が少なくて済みます。 パラレルポート関数ドライバーによって select 要求がデキューされると、ポートの割り当てと IEEE 1284.3 デバイスの選択が試行されます。 クライアントは、許容できるタイムアウト遅延またはその他のデバイス固有の状態が原因で、いつでも選択要求を取り消すことができます。

**注**   クライアントが pparallel\_のみを使用している場合は、 [ **[\_ルーチンコールバック] を選択し\_て**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_select_routine)並列デバイスを選択しようとすると、他のクライアントがパラレルポートに対して競合している (システムによって提供される関数ドライバー)。パラレルポートの場合、クライアントにポートが割り当てられないことがあります。 正常に完了するには、クライアントは[**IOCTL\_内部\_[\_デバイス要求] を選択**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_select_device)する必要があります。 (パラレルポート関数ドライバーはキューに配置され、その後プロセスによって要求が処理されます。また、デバイスの選択要求は、選択したデバイスの要求を受信する順序で処理されます)。

 

パラレルポート関数ドライバーがクライアントの IEEE 1284.3 デバイスを選択すると、クライアントはポートと選択した IEEE 1284.3 デバイスに排他的にアクセスできるようになります。 クライアントは、 [**Pparallel\_選択解除\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_deselect_routine)コールバックを呼び出してポートを解放し、IEEE 1284.3 デバイスの選択を解除する必要があります。 クライアントがポートを解放すると、パラレルポート関数ドライバーは保留中の要求をデキューし、要求を処理します。

Microsoft Windows 2000 では、ポートごとに4つのデイジーチェーンデバイスがサポートされています。ただし、ポートごとに最大2つのデイジーチェーンデバイスを使用することをお勧めします。 Windows XP では、ポートごとに最大2つのデイジーチェーンデバイスがサポートされています。

 

 




