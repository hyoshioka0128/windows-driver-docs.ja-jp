---
title: 記憶域フィルター ドライバーの I/O 要求サポート
description: 記憶域フィルター ドライバーの I/O 要求サポート
ms.assetid: 2899bf91-584f-47fe-9d5c-3feb07b8707e
keywords:
- フィルター ドライバー WDK を記憶域、I/O 要求をサポートします。
- フィルター ドライバー WDK 記憶域、I/O 要求のサポート
- SFD WDK の記憶域、I/O 要求のサポート
- Irp WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61abbe23d0271fa35c1e0dc826349139ddd05cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368190"
---
# <a name="storage-filter-drivers-support-of-io-requests"></a>記憶域フィルター ドライバーの I/O 要求サポート


## <span id="ddk_storage_filter_driver_s_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_SUPPORT_OF_I_O_REQUESTS_KG"></span>


高度な記憶域フィルター ドライバー (SFD) からユーザーのアプリケーションとより高度なドライバーは Irp をインターセプトし、(記憶域クラス ドライバーまたは別のフィルター ドライバー) は、次の下位ドライバーに渡される前に、必要に応じて変更します。 このような SFD に送信または標準以外の形式や、デバイスへの応答をプログラミングでデバイスから返されたデータを変換するなど、特別な処理を必要とする要求のデバイスに固有のサポートを提供する、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求。

下位 SFD はされる Srb や記憶域クラス ドライバーによって発行された Irp を監視し、(記憶域ポート ドライバーまたは別のフィルター ドライバー) は、次の下位ドライバーに渡される前に、必要に応じて変更します。

両方より高いレベルと下位レベル SFDs が下位のドライバーを特別な処理を必要としないすべての I/O 要求を処理できます。

記憶域クラス ドライバーでは、ように、SFD は上位レベルのすべてのカーネル モード ドライバーに共通の次の要件があります。

-   セットを指定する必要があります*ディスパッチ*する I/O マネージャーやドライバーもより高度な Irp を送信する適切な I/O 操作ルーチン。 IRP の同じセットをサポートする必要があります、SFD\_MJ\_の種類のデバイスの記憶域クラス ドライバーとして XXX。

-   [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求すると、その物理デバイスが処理できるよう多くのクラス ドライバーでサポートされている I/O 制御コードをサポートし、、可能であれば、ドライバーで、残りの I/O 制御コードのサポートをエミュレートします。

-   必要があります、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン、 [*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチン、および*ディスパッチ*を処理するルーチン PnP Irp の電源し、任意の他の標準的な高度なドライバーのルーチンなどがあることができます[ *IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンは、必要に応じて。

-   PnP 処理、電源管理、およびシステム コントロール Irp の規則に従う必要があります。

そのデバイスに特殊な機能がある場合、SFD が I/O 制御コードのドライバーの定義済みの I/O 制御コードをデバイス固有の種類のシステムに必要な設定に加えてのセットをサポートできます[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求。

 

 




