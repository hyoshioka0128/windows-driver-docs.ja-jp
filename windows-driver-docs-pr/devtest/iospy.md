---
title: IoSpy
description: IoSpy は、デバイスのカーネル モード ドライバーに対して行われた IOCTL および WMI の要求に関するデータを記録するフィルター ドライバーです。
ms.assetid: 5fe52fe6-97b4-477a-9450-727c5bf9bd72
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9446da21ab50fd7e7ef8dceeba7114f83f622a7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373702"
---
> [!NOTE]
> IoSpy と IoAttack は Windows 10 バージョン 1703 後は WDK に含まれて使用できなくします。
>
> これらのツールを別の方法として、HLK で使用可能なファジー化のテストを使用して検討してください。 次に考慮すべきいくつか示します。
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
> 使用することも、[カーネル同期遅延ファジー テスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)Driver Verifier に含まれます。
>



# <a name="iospy"></a>IoSpy


IoSpy は、デバイスのカーネル モード ドライバーに対して行われた IOCTL および WMI の要求に関するデータを記録するフィルター ドライバーです。

インストールして IoSpy を使用して削除する、[侵入テスト (デバイスの基本)](coverage-tests--device-fundamentals-.md)テスト、 **I/O スパイを有効にする**と**I/O スパイを無効にする**します。 *DQ*パラメーターは、IoSpy フィルター ドライバーがインストールされているデバイスを制御します。 IoSpy IOCTL および WMI 要求内で詳細を記録する、 [IoSpy データ ファイル](#iospy-data-file)が使用する[IoAttack](ioattack.md)ファジーを実行するには、テストします。

**重要な**  IoSpy を以前実行が必要があるあり、テスト システムから削除された IoAttack を実行する前にします。 詳細については、次を参照してください。 [IoSpy IoAttack と実行のファジー テスト方法](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)します。

 

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
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>I/O スパイを無効にします。</p></td>
<td align="left"><p>1 つ以上のデバイスでの I/O スパイを無効にします。 IoSpy をアンインストールし、IOCTL と WMI フィルターをテスト システム上のすべてのデバイスを無効にします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_DisableSupport.wsc</p>
<p><strong>メソッドをテストします。</strong>DisableIoSpy</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_I_O_Spy-enabled_Device"></span><span id="display_i_o_spy-enabled_device"></span><span id="DISPLAY_I_O_SPY-ENABLED_DEVICE"></span>I/O Spy が有効なデバイスを表示します。</p></td>
<td align="left"><p>有効にする I/O スパイを持つデバイスを表示します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_DisplayEnabledDevices.wsc</p>
<p><strong>メソッドをテストします。</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>I/O スパイを有効にします。</p></td>
<td align="left"><p>テスト システムで IoSpy をインストールし、IOCTL および WMI の 1 つまたは複数のデバイスでフィルター処理を有効にします。 DQ パラメーターは、IoSpy フィルター ドライバーのインストールはデバイスを制御します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_IOSpy_EnableSupport.wsc</p>
<p><strong>メソッドをテストします。</strong>EnableIoSpy</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> - IoSpy データ ファイルへのパスを指定します。 既定の場所は %SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
</tbody>
</table>

 

## <a name="iospy-data-file"></a>IoSpy データ ファイル

IoSpy のテスト システムのインストール後に、ファジー テストを有効になっているデバイスのドライバーに IOCTL および WMI の要求を送信するデータを記録します。 IoSpy では、これらの要求のペイロードは分析されません、中には、ペイロードのバッファーの長さなどの要求の詳細を記録します。

*DFD*のパラメーター、**を有効にする I/O スパイ**テスト IoSpy データ ファイルへのパスを指定します。 既定の場所は %systemdrive%\\DriverTest\\IoSpy

 

 





