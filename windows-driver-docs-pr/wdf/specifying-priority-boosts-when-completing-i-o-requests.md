---
title: I/O 要求完了時の優先度引き上げの指定
description: I/O 要求完了時の優先度引き上げの指定
ms.assetid: 9a501ca1-58c9-4458-b202-9581f8ce5e5f
keywords:
- 要求の処理 WDK KMDF、優先度のブースト
- 優先度を上げる WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c8098efd572c9be60b320f598e3392a5ab943f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842190"
---
# <a name="specifying-priority-boosts-when-completing-io-requests"></a>I/O 要求完了時の優先度引き上げの指定


ドライバーは、i/o 要求を完了すると、 [**Wdfrequestcompletewithpriority ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)を呼び出して、i/o 操作を要求したスレッドの実行時の優先順位を上げるためにシステムで使用される値を指定できます。

ドライバーが[**Wdfrequestcompletewith優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)ではなく Wdfrequestcomplete または[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)を呼び出した場合、フレームワークはデバイスの種類に基づく既定の priority boost 値を使用します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 次の表は、フレームワークが使用する既定の priority boost の値を示しています。 デバイスの種類と priority boost 定数は、 *Wdm*で定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスの種類</th>
<th align="left">既定の優先度ブースト</th>
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

 

 

 





