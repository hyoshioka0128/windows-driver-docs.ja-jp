---
title: ファイルシステムフィルタードライバーとデバイスドライバーの違い
description: ファイルシステムフィルタードライバーとデバイスドライバーの違い
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- フィルタードライバー WDK ファイルシステム、およびデバイスドライバー
- ファイルシステムフィルタードライバー WDK、およびデバイスドライバー
- デバイスドライバー WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be82c51832c5ff1a7eef2a0f00378030d560c608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841219"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>ファイルシステムフィルタードライバーとデバイスドライバーの違い


## <span id="ddk_how_file_system_filter_drivers_are_different_from_device_drivers_i"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_DIFFERENT_FROM_DEVICE_DRIVERS_I"></span>


次のサブセクションでは、ファイルシステムフィルタードライバーとデバイスドライバーの違いについて説明します。

### <a name="span-idno_power_managementspanspan-idno_power_managementspanspan-idno_power_managementspanno-power-management"></a><span id="No_Power_Management"></span><span id="no_power_management"></span><span id="NO_POWER_MANAGEMENT"></span>電源管理なし

ファイルシステムフィルタードライバーはデバイスドライバーではないため、ハードウェアデバイスを直接制御しないため、 [**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求を受信しません。 代わりに、電力 Irp はストレージデバイススタックに直接送信されます。 ただし、まれに、ファイルシステムフィルタードライバーによって電源管理が妨げられることがあります。 このため、ファイルシステムフィルタードライバーは、 **Driverentry**ルーチンで IRP\_MJ\_電源のディスパッチルーチンを登録する必要がありません。また、 [poxxx](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)ルーチンを呼び出すことはできません。

### <a name="span-idno_wdmspanspan-idno_wdmspanspan-idno_wdmspanno-wdm"></a><span id="No_WDM"></span><span id="no_wdm"></span><span id="NO_WDM"></span>WDM なし

ファイルシステムフィルタードライバーを Windows Driver Model (WDM) ドライバーにすることはできません。 Microsoft [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)は、デバイスドライバーのみを対象としています。 Windows Me、Windows 98、および Windows 95 でのファイルシステムドライバーの開発の詳細については、「Windows Me Driver Development Kit (DDK)」を参照してください。

### <a name="span-idno_adddevice_or_startiospanspan-idno_adddevice_or_startiospanspan-idno_adddevice_or_startiospanno-adddevice-or-startio"></a><span id="No_AddDevice_or_StartIo"></span><span id="no_adddevice_or_startio"></span><span id="NO_ADDDEVICE_OR_STARTIO"></span>AddDevice または StartIo はありません

ファイルシステムフィルタードライバーはデバイスドライバーではないため、ハードウェアデバイスを直接制御しないので、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)または[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを指定しないでください。

### <a name="span-iddifferent_device_objects_createdspanspan-iddifferent_device_objects_createdspanspan-iddifferent_device_objects_createdspandifferent-device-objects-created"></a><span id="Different_Device_Objects_Created"></span><span id="different_device_objects_created"></span><span id="DIFFERENT_DEVICE_OBJECTS_CREATED"></span>作成されたさまざまなデバイスオブジェクト

ファイルシステムフィルタードライバーとデバイスドライバーは両方ともデバイスオブジェクトを作成しますが、作成するデバイスオブジェクトの数と種類は異なります。

デバイスドライバーは、デバイスを表す物理デバイスオブジェクトと機能デバイスオブジェクトを作成します。 プラグアンドプレイ (PnP) マネージャーは、デバイスドライバーによって作成されたすべてのデバイスオブジェクトを含むグローバルデバイスツリーを構築し、管理します。 ファイルシステムフィルタードライバーによって作成されたデバイスオブジェクトは、このデバイスツリーに含まれていません。

ファイルシステムフィルタードライバーは、物理的または機能しているデバイスオブジェクトを作成しません。 代わりに、コントロールデバイスオブジェクトを作成し、デバイスオブジェクトをフィルター処理します。 *コントロールデバイスオブジェクト*は、システムおよびユーザーモードアプリケーションに対するフィルタードライバーを表します。 *フィルターデバイスオブジェクト*は、特定のファイルシステムまたはボリュームをフィルター処理する実際の作業を実行します。 通常、ファイルシステムフィルタードライバーは、1つのコントロールデバイスオブジェクトと1つまたは複数のフィルターデバイスオブジェクトを作成します。

### <a name="span-idother_differencesspanspan-idother_differencesspanspan-idother_differencesspanother-differences"></a><span id="Other_Differences"></span><span id="other_differences"></span><span id="OTHER_DIFFERENCES"></span>その他の相違点

ファイルシステムフィルタードライバーはデバイスドライバーではないため、[ダイレクトメモリアクセス (DMA)](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o-with-dma)は実行されません。

デバイスフィルタードライバーは、ターゲットデバイスの関数ドライバーの上または下にアタッチできますが、ファイルシステムフィルタードライバーは、ターゲットファイルシステムドライバーの上にしかアタッチできません。 したがって、デバイスドライバーの用語では、ファイルシステムフィルタードライバーは上位フィルターに限らず、フィルターを下げることはできません。

 

 




