---
title: ハードウェア リソースの検索とマッピング
description: このトピックでは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーまたはユーザーモードドライバーフレームワーク (UMDF) ドライバーが、EvtdeviceCmResourceTypeMemory ハードウェアコールバックで受信した変換済みメモリリソース () をマップする方法について説明します。プロシージャ.
ms.assetid: 9D65D70C-FFF1-4663-8701-221C5443C425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b9ca351a9b13b5d201b2ca37b794afb6f1a453
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842854"
---
# <a name="finding-and-mapping-hardware-resources"></a>ハードウェア リソースの検索とマッピング


このトピックでは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーまたはユーザーモードドライバーフレームワーク (UMDF) ドライバーが、 [*EvtdeviceCmResourceTypeMemory ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で受信した変換後のメモリリソース () をマップする方法について説明します。

この種類のリソースは、 [**IPnpCallbackHardware2:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)メソッドでも使用できます。 詳細については、「 [UMDF 1.X ドライバーでのハードウェアリソースの検索とマッピング](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)」を参照してください。

ドライバーは、デバイスのリソースリストに含まれているハードウェアリソースの[*Evtdeviceロウハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で、[生および翻訳](raw-and-translated-resources.md)されたバージョンを受け取ります。 ドライバーはリソースリストを保存できます。これは、フレームワークがドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数を呼び出すまで有効です。

通常、ドライバーは、 [**WdfCmResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetcount)を呼び出し[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)て、変換されたリソースリスト内のリソース記述子の数を特定します。次に、ループで[**Wdfcmresourcelistgetdescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistgetdescriptor)を呼び出して、メモリマップトレジスタ、i/o ポート、および割り込みを識別します。

ドライバーに変換されたメモリリソース (**CmResourceTypeMemory**) が割り当てられている場合、その物理アドレスを、デバイスレジスタにアクセスできるアドレスにマップする必要があります。

KMDF ドライバーは、 [**Mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)を呼び出して、指定された物理アドレス範囲を非ページシステム領域にマップします。 次に、 [**HAL ライブラリルーチン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を使用して、レジスタの読み取りと書き込みを行います。

UMDF ドライバーは、 [**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)を呼び出して、物理アドレスを[WDF Register/Port Access 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/)と組み合わせて使用して、レジスタとポートの読み取りと書き込みを行うことができる擬似ベースアドレスに割り当てます。

ドライバーは、 [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数から[**mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)または[**wdfdeviceunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace)を呼び出すことによって、リソースを解除します。

I/o スペース (**Cmresourcetypeport**、 **cmresourcetypeport**、 **CmResourceTypeDma**) にリソースをマップする必要はありません。

UMDF ドライバーが[**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)を呼び出す場合は、 **UmdfDirectHardwareAccess** INF ディレクティブを**AllowDirectHardwareAccess**に設定する必要があります。

ドライバーがメモリマップトレジスタリソースを検出してマップする方法を示す例については、「[デバイスレジスタの読み取りと書き込み」を](reading-and-writing-to-device-registers.md)参照してください。

 

 





