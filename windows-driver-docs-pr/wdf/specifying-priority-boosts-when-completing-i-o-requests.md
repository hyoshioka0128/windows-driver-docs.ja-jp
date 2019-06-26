---
title: I/O 要求完了時の優先度引き上げの指定
description: I/O 要求完了時の優先度引き上げの指定
ms.assetid: 9a501ca1-58c9-4458-b202-9581f8ce5e5f
keywords:
- 要求処理の WDK KMDF、優先度の実行
- 優先順位の WDK KMDF ブーストします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2a30d15f8209943c94f0fb4ac89b2cbe3887491
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382361"
---
# <a name="specifying-priority-boosts-when-completing-io-requests"></a>I/O 要求完了時の優先度引き上げの指定


呼び出すことができます、ドライバーでは、I/O 要求が完了したら、 [ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)システムは、I/O を要求したスレッドの実行時の優先度を上げるを使用して値を指定するには操作です。

ドライバーを呼び出す場合[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)または[ **WdfRequestCompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)の代わりに[ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)フレームワークは、デバイスの種類に基づく既定の優先度のブースト値を使用します。 次の表では、フレームワークを使用して既定の優先度のブースト値を示します。 デバイスの種類および優先順位 boost 定数で定義されて*Wdm.h*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスの種類</th>
<th align="left">既定の Priority Boost</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_UNDEFINED</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_BEEP</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CD_ROM</p></td>
<td align="left"><p>IO_CD_ROM_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_CD_ROM_FILE_SYSTEM</p></td>
<td align="left"><p>IO_CD_ROM_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CONTROLLER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DATALINK</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DFS</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DISK</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DISK_FILE_SYSTEM</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_INPORT_PORT</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KEYBOARD</p></td>
<td align="left"><p>IO_KEYBOARD_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MAILSLOT</p></td>
<td align="left"><p>IO_MAILSLOT_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MIDI_IN</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MIDI_OUT</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MOUSE</p></td>
<td align="left"><p>IO_MOUSE_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MULTI_UNC_PROVIDER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NAMED_PIPE</p></td>
<td align="left"><p>IO_NAMED_PIPE_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NETWORK_BROWSER</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NULL</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_PARALLEL_PORT</p></td>
<td align="left"><p>IO_PARALLEL_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_PHYSICAL_NETCARD</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_PRINTER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SCANNER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SERIAL_MOUSE_PORT</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SERIAL_PORT</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SCREEN</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SOUND</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_STREAMS</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_TAPE</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_TAPE_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_TRANSPORT</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_UNKNOWN</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_VIDEO</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_VIRTUAL_DISK</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_WAVE_IN</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_WAVE_OUT</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_8042_PORT</p></td>
<td align="left"><p>IO_KEYBOARD_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK_REDIRECTOR</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_BATTERY</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_BUS_EXTENDER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MODEM</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_VDM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MASS_STORAGE</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SMB</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KS</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CHANGER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SMARTCARD</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_ACPI</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DVD</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_FULLSCREEN_VIDEO</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DFS_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DFS_VOLUME</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SERENUM</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_TERMSRV</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KSEC</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_FIPS</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_INFINIBAND</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
</tbody>
</table>

 

 

 





