---
title: ディスプレイ INF ファイルのセクション
description: ディスプレイ INF ファイルのセクション
ms.assetid: 2075a10f-a504-4bdc-8112-9c583c5084bb
keywords:
- sideband での WDK Windows 2000 ディスプレイのアドレス指定
- AGP 転送率 WDK Windows 2000 ディスプレイ
- ソフトウェア設定セクション
- CapabilityOverride
- INF ファイル WDK Windows 2000 display
- INF ファイルセクションの表示 WDK Windows 2000 display
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f22d7938de2acbe4181a5e9e4bc949f62713be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839742"
---
# <a name="display-inf-file-sections"></a>ディスプレイ INF ファイルのセクション


## <span id="ddk_display_inf_file_sections_gg"></span><span id="DDK_DISPLAY_INF_FILE_SECTIONS_GG"></span>


このセクションでは、グラフィックスアダプターのインストールに特に適用されるセットアップ情報ファイル (INF) のセクションを記述する方法について説明します。 INF ファイルの一般的な情報については、「 [Inf ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。

### <a name="span-idddinstallsoftwaresettings_sectionspanspan-idddinstallsoftwaresettings_sectionspanspan-idddinstallsoftwaresettings_sectionspanddinstallsoftwaresettings-section"></a><span id="DDInstall.SoftwareSettings_Section"></span><span id="ddinstall.softwaresettings_section"></span><span id="DDINSTALL.SOFTWARESETTINGS_SECTION"></span>DDInstall. ソフトウェア設定セクション

*Ddinstall*。 **[ソフトウェアの設定]** セクションに、 [**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)ディレクティブ、または[**delreg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブが含まれています。 各ディレクティブは、追加または削除するインストーラーのレジストリエントリを含む、ライターによって定義された別の INF セクションを指します。

たとえば、次のコードは、 **AddReg**ディレクティブを示しています。このディレクティブは、 **ACME-1234\_devicedevicesettings**という名前のライター定義の add registry セクションを指します。 **Delreg**ディレクティブは、 **ACME-1234\_DeleteSWSettings**という名前の削除レジストリセクションを指します。

```inf
[ACME-1234.SoftwareSettings]
AddReg=ACME-1234_SoftwareDeviceSettings
DelReg=ACME-1234_DeleteSWSettings
```

[レジストリの追加] セクションでは、次のコードに示すように、レジストリに4つのエントリを追加し、値を設定します。

```inf
[ACME-1234_SoftwareDeviceSettings]
HKR,, InstalledDisplayDrivers, %REG_MULTI_SZ%, Acme1
HKR,, OverRideMonitorPower, %REG_DWORD%, 0
HKR,, MultiFunctionSupported, %REG_DWORD%, 1
HKR,, VideoDebugLevel, %REG_DWORD%, 2
```

前のコードでは、最初に、**によって**、表示ドライバーの名前に対して、その値が設定されています。 次に、このコードでは、 **Overridemonitorpower** entry の値を0に設定します (つまり、 **FALSE**)。 このエントリは、OEM システムベンダーだけが使用する必要があります。モニターデバイス (LCD、CRT、TV など) の電源動作を制御します。 1に設定すると、 **Overridemonitorpower**によってモニターデバイスの電源状態が D0 および D3 に制限されます。

3番目のコードでは、 **Multifunctionsupported**エントリの値を 1 (つまり、 **TRUE**) に設定しています。これは、複数の PCI 関数をサポートするアダプターに必要な値です。 最後に、コードは**Videodebuglevel**エントリの値を設定します。これは、チェックされたビルドがデバッグメッセージに使用するグローバルデバッグレベルを制御します。 この値の範囲は、0 (デバッグメッセージなし) から 3 (最も詳細なメッセージ) です。 グローバルデバッグレベルの詳細については、「 [**Videodebugprint**](https://docs.microsoft.com/previous-versions/ff570170(v=vs.85))」を参照してください。

ほとんどのビデオミニポートドライバーは、VGA 互換ではなく、レジストリに**VgaCompatible**エントリを必要としません。 ビデオミニポートドライバーが VGA と互換性がある場合は、次に示すように、レジストリに**VgaCompatible**エントリを追加し、[レジストリの追加] セクションで値を 1 (**TRUE**) に設定します。

```registry
[ACME-1234_SoftwareDeviceSettings]
HKR,, VgaCompatible, %REG_DWORD%, 1
```

VGA と互換性のあるビデオミニポートドライバーの詳細については、「 [Vga 互換ビデオミニポートドライバー (Windows 2000 モデル)](vga-compatible-video-miniport-drivers--windows-2000-model-.md)」を参照してください。

次の GraphicsClocking セクションでは、3つのレジストリエントリ (、 **Memclocking**、 **CapabilityOverride**) を削除します。

```inf
[ACME-1234_DeleteSWSettings]
HKR,, GraphicsClocking
HKR,, MemClocking
HKR,, CapabilityOverride
```

**CapabilityOverride**エントリは、ディスプレイドライバーのシステムの電源をオフにする機能を指定します。 たとえば、表示ドライバーが[**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)関数を実装している場合でも、 **CapabilityOverride**エントリに0x10 フラグが設定されていると、その機能は使用できません。

**CapabilityOverride**レジストリエントリの値は、次の表に示す1つ以上のフラグのビットごとの or です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>すべてのハードウェアアクセラレータを無効にします。 ハードウェアアクセラレータのスライドバー (コントロールパネルの<strong>表示</strong>項目) を最小値に移動することと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Microsoft DirectDraw および Microsoft Direct3D ハードウェアアクセラレータのすべてのサポートを無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>Direct3D ハードウェアアクセラレータのすべてのサポートを無効にします。 は、ドライバーに到達<em>するために</em>Direct3D の機能とコールバック情報を要求する<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>ddgetdriverinfo</strong></a>を呼び出しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>OpenGL インストール可能なクライアントドライバー (ICD) と miniclient driver (MCD) のすべてのサポートを無効にします。 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"><strong>DrvSetPixelFormat</strong></a>、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"><strong>DrvDescribePixelFormat</strong></a>、および<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)"><strong>DrvSwapBuffers</strong></a>への呼び出しがドライバーに到達しないようにします。 では、OPENGL_GETINFO、OPENGL_CMD および MCDFUNCS のエスケープがドライバーに到達しないようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>ドライバー内のすべてのエスケープのサポートを無効にします。 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a>と<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a>の呼び出しがドライバーに到達しないようにします。</p></td>
</tr>
</tbody>
</table>

 

Windows に付属しているディスプレイドライバーの場合、 **CapabilityOverride**は通常、"0x8" に設定されます。これにより、OpenGL が無効になります。 0x10 フラグを設定して OpenGL を無効にする必要はないことに注意してください。すべてのエスケープを無効にする場合を除き、0x10 フラグは設定しないでください。

Microsoft Windows XP およびそれ以前のオペレーティングシステムでは、ディスプレイドライバーが更新されたときに**CapabilityOverride**レジストリエントリは削除されません。たとえば、Windows に付属しているドライバーから、独立系ハードウェアベンダー (IHV) によって提供されたより新しいドライバーに更新された場合などです。 Persistent **CapabilityOverride**エントリは、古いドライバーで無効にした更新されたドライバーの同じ機能を無効にします。 そのため、Windows XP およびそれ以前のバージョンでは、既存の**CapabilityOverride**エントリを明示的に削除する**DELREG**ディレクティブを INF ファイルに追加します。 Windows XP SP1 以降のオペレーティングシステムでは、ドライバーが更新されたときに**CapabilityOverride**エントリが自動的に削除されます。そのため、これらのシステムでは、 **CapabilityOverride**エントリを削除する必要はありません。

### <a name="span-iddisabling_agp_transfer_rates_and_sideband_addressingspanspan-iddisabling_agp_transfer_rates_and_sideband_addressingspanspan-iddisabling_agp_transfer_rates_and_sideband_addressingspandisabling-agp-transfer-rates-and-sideband-addressing"></a><span id="Disabling_AGP_Transfer_Rates_and_Sideband_Addressing"></span><span id="disabling_agp_transfer_rates_and_sideband_addressing"></span><span id="DISABLING_AGP_TRANSFER_RATES_AND_SIDEBAND_ADDRESSING"></span>AGP 転送率と Sideband のアドレス指定の無効化

必要に応じて、ディスプレイアダプターの INF ファイルを変更して、特定の AGP 転送率または sideband のアドレス指定を無効にすることができます。 ミニポートドライバーは[**AgpSetRate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_set_rate)を呼び出すときに AGP 転送速度を変更することができますが、このような呼び出しでは、INF ファイルで無効になっている転送速度を変更することはできません。

Windows Driver Kit (WDK) に付属している*regstr .h*ヘッダーファイルでは、次のフラグのセットが定義されています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_1X_RATE</p></td>
<td align="left"><p>0x00000001L</p></td>
<td align="left"><p>1倍速 (66 MHz) の転送速度を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_2X_RATE</p></td>
<td align="left"><p>0x00000002L</p></td>
<td align="left"><p>1倍速転送速度の2倍を無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_4X_RATE</p></td>
<td align="left"><p>0x00000004L</p></td>
<td align="left"><p>1倍速転送速度の4倍を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_8X_RATE</p></td>
<td align="left"><p>0x00000008L</p></td>
<td align="left"><p>単一速度の転送速度の8倍を無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_SBA_ENABLE</p></td>
<td align="left"><p>0x00000100L</p></td>
<td align="left"><p>Sideband アドレス指定 (SBA) を無効にします。</p></td>
</tr>
</tbody>
</table>

 

グローバルとプラットフォーム固有の2種類の設定があります。 レジストリには、次の場所にあるグローバルエントリが格納されます。

```registry
HKLM,"SYSTEM\CurrentControlSet\Control\AGP"
```

プラットフォーム固有のエントリは、フィルタードライバーサービスキーの "Parameters" の下にあります。 たとえば、次のレジストリの場所にある架空の AcmeAGP アダプターに対して、これらのエントリが存在します。

```registry
HKLM,"SYSTEM\CurrentControlSet\Services\AcmeAGP\Parameters"
```

DeviceID が 0x012A (Nuclear3D) で、VendorID が0x1AD0 であるデバイスの sideband アドレス指定を無効にするには、 **Nuclear3D\_Install. HW**セクションを INF ファイルに追加します。 (この種類の INF インストールセクションの詳細については、「 [**Inf DDInstall. HW」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)を参照してください)。このセクションでは、次のような[**AddReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)ディレクティブを追加します。

```inf
[Nuclear3D_Install.HW] 
AddReg = Nuclear3D_Reg 
```

次に、 **AddReg**ディレクティブが指す次のセクションを作成します。

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
```

上記のエントリは、HKLM の下にある文字列によって識別されるサブキーがレジストリに追加されることを示しています。これは、HKEY\_ローカル\_マシンのルートにあります。 "1AD0012A" 文字列はエントリ名で、最初の4文字が DeviceID を構成し、最後の4文字がこのパートの VendorID を構成します。 エントリ名の後に続く16進数は、エントリのデータ型を示す一連のフラグで構成されます。 最後の部分はエントリ値です。これにより、sideband のアドレス指定が無効になります。

**重要**   [値] エントリのバイトは、前の表の\_\_SBA\_ENABLE フラグの定義とは逆の\_順序になっています。

 

この同じデバイスのすべてのチップセットで AGP 4 が破損していると判断したとします。 この事実を示すには、Nuclear3D\_Reg セクションに2番目のエントリを追加します。

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
HKLM,"SYSTEM\CurrentControlSet\Control\AGP","1AD0012A",0x00030003,04,00,00,00,00,00,00,00 
```

上記のコードの2番目のエントリは、HKLM の下にある文字列によって識別されるサブキーがレジストリに追加されることを示します。これは、HKEY\_ローカル\_マシンのルートにあります。 前のエントリと同様に、このサブキーに関連付けられている値の名前は、デバイスの DeviceID と VendorID で構成される文字列です。 フラグの値も同じです。 値のエントリは AGP\_フラグ\_4 × 4\_率\_ないため、AGP 4 の転送速度を無効にします。 前と同様に、この値エントリのバイトは、前の表のフラグの値と逆の順序になっています。

 

 





