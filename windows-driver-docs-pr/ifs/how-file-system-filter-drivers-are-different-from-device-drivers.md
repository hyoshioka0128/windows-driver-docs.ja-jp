---
title: ファイル システム フィルター ドライバーとデバイス ドライバーの相違点
description: ファイル システム フィルター ドライバーとデバイス ドライバーの相違点
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- フィルター ドライバー WDK ファイル システム、デバイス ドライバーとの比較
- ファイル システム フィルター ドライバー WDK、デバイス ドライバーとの比較
- デバイス ドライバー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8212824fced83564cab1400c9cd5c5aa0b82dee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379070"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>ファイル システム フィルター ドライバーとデバイス ドライバーの相違点


## <span id="ddk_how_file_system_filter_drivers_are_different_from_device_drivers_i"></span><span id="DDK_HOW_FILE_SYSTEM_FILTER_DRIVERS_ARE_DIFFERENT_FROM_DEVICE_DRIVERS_I"></span>


次のサブセクションでは、ファイル システム フィルター ドライバーとデバイス ドライバーの間の違いの一部について説明します。

### <a name="span-idnopowermanagementspanspan-idnopowermanagementspanspan-idnopowermanagementspanno-power-management"></a><span id="No_Power_Management"></span><span id="no_power_management"></span><span id="NO_POWER_MANAGEMENT"></span>電源管理

受信はないため、ファイル システム フィルター ドライバーは、デバイス ドライバーがないし、したがって制御しないデバイスのハードウェア直接、 [ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求。 代わりに、電源の Irp では、記憶域デバイス スタックに直接送信されます。 まれに、ただし、ファイル システム フィルター ドライバー干渉する可能性が電源管理を使用します。 このため、ファイル システム フィルター ドライバーは登録ディスパッチ ルーチン IRP の\_MJ\_で電源、 **DriverEntry**ルーチンを呼び出す必要はありません[PoXxx](https://msdn.microsoft.com/library/windows/hardware/ff559835)ルーチン。

### <a name="span-idnowdmspanspan-idnowdmspanspan-idnowdmspanno-wdm"></a><span id="No_WDM"></span><span id="no_wdm"></span><span id="NO_WDM"></span>WDM なし

ファイル システム フィルター ドライバーは、Windows Driver Model (WDM) ドライバーをすることはできません。 Microsoft [Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698)デバイス ドライバーに対してだけです。 Windows Me、Windows 98、および Windows 95 でファイル システム ドライバーの開発の詳細については、Windows Me ドライバー開発キット (DDK) を参照してください。

### <a name="span-idnoadddeviceorstartiospanspan-idnoadddeviceorstartiospanspan-idnoadddeviceorstartiospanno-adddevice-or-startio"></a><span id="No_AddDevice_or_StartIo"></span><span id="no_adddevice_or_startio"></span><span id="NO_ADDDEVICE_OR_STARTIO"></span>AddDevice または StartIo なし

したがって制御しないデバイスのハードウェア直接ファイル システム フィルター ドライバーがデバイス ドライバーがないためは必要ありません[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)または[ **StartIo**](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。

### <a name="span-iddifferentdeviceobjectscreatedspanspan-iddifferentdeviceobjectscreatedspanspan-iddifferentdeviceobjectscreatedspandifferent-device-objects-created"></a><span id="Different_Device_Objects_Created"></span><span id="different_device_objects_created"></span><span id="DIFFERENT_DEVICE_OBJECTS_CREATED"></span>別のデバイス オブジェクトの作成

ファイル システム フィルター ドライバーとデバイス ドライバーは、デバイス オブジェクトを作成して、自分で作成したデバイス オブジェクトの種類と数が異なります。

デバイス ドライバーは、物理および機能のデバイスのデバイスを表すオブジェクトを作成します。 プラグ アンド プレイ (PnP) マネージャーでは、ビルドし、デバイス ドライバーによって作成されたすべてのデバイスを含むグローバル デバイス ツリーのオブジェクトを保持します。 ファイル システム フィルター ドライバーを作成するデバイス オブジェクトは、このデバイス ツリーに含まれていません。

ファイル システム フィルター ドライバーは、物理または機能のデバイス オブジェクトを作成できません。 代わりに、デバイス オブジェクトにコントロールを作成し、デバイス オブジェクトをフィルター処理します。 *制御デバイス オブジェクト*システムおよびユーザー モード アプリケーションには、フィルター ドライバーを表します。 *フィルター デバイス オブジェクト*特定のファイル システム ボリュームまたはボリュームをフィルター処理の実際の作業を実行します。 1 つは、ファイル システム フィルター ドライバーが通常作成制御デバイス オブジェクトと 1 つ以上のデバイス オブジェクトをフィルター処理します。

### <a name="span-idotherdifferencesspanspan-idotherdifferencesspanspan-idotherdifferencesspanother-differences"></a><span id="Other_Differences"></span><span id="other_differences"></span><span id="OTHER_DIFFERENCES"></span>その他の違い

実行しないファイル システム フィルター ドライバーはデバイス ドライバーではないため、[ダイレクト メモリ アクセス (DMA)](https://msdn.microsoft.com/library/windows/hardware/ff565374)します。

デバイス フィルター ドライバーは、ターゲット デバイスの機能のドライバーより上または下をアタッチすることができますとは異なり、ファイル システム フィルター ドライバーは、対象のファイル システム ドライバーの上にのみアタッチできます。 したがって、デバイス ドライバーには、ファイル システム フィルター ドライバーは、上部のフィルターのみ、フィルターが低いことはありませんをすることができます。

 

 




