---
title: IoSpy
description: IoSpy は、デバイスのカーネルモードドライバーに対して行われた IOCTL および WMI 要求に関するデータを記録するフィルタードライバーです。
ms.assetid: 5fe52fe6-97b4-477a-9450-727c5bf9bd72
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: c000ef6d8e4ccdfa3f29840f495c8bde893db531
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235291"
---
# <a name="iospy"></a>IoSpy

> [!NOTE]
> IoSpy と Iospy は、Windows 10 バージョン1703以降の WDK では利用できなくなりました。
>
> これらのツールの代わりに、HLK で使用可能なファジーテストの使用を検討してください。 次に、考慮すべき点をいくつか示します。
> 
> [DF - ランダム IOCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF - サブオープンのファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF - 0 長バッファー FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF - ランダム FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF - Misc API のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> また、ドライバー検証ツールに含まれている[カーネル同期遅延ファジー化](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)を使用することもできます。
>

IoSpy は、デバイスのカーネルモードドライバーに対して行われた IOCTL および WMI 要求に関するデータを記録するフィルタードライバーです。

IoSpy は、[侵入テスト (デバイスの基礎)](coverage-tests--device-fundamentals-.md)テストを使用してインストールおよび削除したり、 **I/o Spy を有効に**したり、 **i/o spy を無効**にしたりすることができます。 *DQ*パラメーターは、iospy フィルタードライバーがインストールされているデバイスを制御します。 IoSpy は、 [iospy データファイル](#iospy-data-file)内の IOCTL および WMI 要求に関する詳細を記録します。このファイルは、 [iospy](ioattack.md)によって、ファジーテストを実行するために使用されます。

**重要**   IoAttack を実行する前に、Ioattack を実行し、それをテストシステムから削除する必要があります。 詳細については、「 [IoSpy と Iospy でファジーテストを実行する方法](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)」を参照してください。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>I/o Spy を無効にする</p></td>
<td align="left"><p>1つ以上のデバイスで i/o Spy を無効にします。 IoSpy をアンインストールし、テストシステム上のすべてのデバイスの IOCTL および WMI フィルター処理を無効にします。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_DisableSupport</p>
<p><strong>テストメソッド:</strong>DisableIoSpy</p>
<p><strong>パラメーター:</strong> -「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照してください。</p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_I_O_Spy-enabled_Device"></span><span id="display_i_o_spy-enabled_device"></span><span id="DISPLAY_I_O_SPY-ENABLED_DEVICE"></span>I/o Spy 対応デバイスを表示する</p></td>
<td align="left"><p>I/o Spy が有効になっているデバイスを表示します。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_DisplayEnabledDevices</p>
<p><strong>テストメソッド:</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>I/o Spy を有効にする</p></td>
<td align="left"><p>テストシステムに IoSpy をインストールし、1つまたは複数のデバイスで IOCTL および WMI フィルタリングを有効にします。 DQ パラメーターは、IoSpy フィルタードライバーがインストールされるデバイスを制御します。</p>
<p><strong>テストバイナリ:</strong>Devfund_IOSpy_EnableSupport</p>
<p><strong>テストメソッド:</strong>EnableIoSpy</p>
<p><strong>パラメーター:</strong> -「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照してください。</p>
<p><em>DQ</em></p>
<p><em>DFD</em> -IoSpy データファイルへのパスを指定します。 既定の場所は%SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
</tbody>
</table>

 

## <a name="iospy-data-file"></a>IoSpy データファイル

IoSpy はテストシステムにインストールされた後、IOCTL および WMI 要求によって送信されたデータを、ファジーテストが有効になっているデバイスのドライバーに記録します。 IoSpy は、これらの要求のペイロードを分析しませんが、ペイロードバッファーの長さなどの要求の詳細を記録します。

**Enable I/o spy**テストの*DFD*パラメーターでは、iospy データファイルへのパスを指定します。 既定の場所は% SystemDrive% \\ drivertest \\ iospy です

 

 





