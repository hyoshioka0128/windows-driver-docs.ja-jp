---
title: ディスプレイ INF ファイルのセクション
description: ディスプレイ INF ファイルのセクション
ms.assetid: 2075a10f-a504-4bdc-8112-9c583c5084bb
keywords:
- Windows 2000 の WDK の表示をアドレス指定側波帯
- 転送率の AGP WDK Windows 2000 を表示します。
- SoftwareSettings セクション
- CapabilityOverride
- Windows 2000 の WDK の INF ファイルを表示します。
- INF ファイルのセクションでは Windows 2000 の WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37cad16e0acf7f77a5c116454b6260b20dccb7a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365754"
---
# <a name="display-inf-file-sections"></a>ディスプレイ INF ファイルのセクション


## <span id="ddk_display_inf_file_sections_gg"></span><span id="DDK_DISPLAY_INF_FILE_SECTIONS_GG"></span>


このセクションでは、具体的には、グラフィックス アダプターのインストールに適用されます (INF) のセクションで、セットアップ情報ファイルを記述する方法を指示します。 INF ファイルの概要については、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

### <a name="span-idddinstallsoftwaresettingssectionspanspan-idddinstallsoftwaresettingssectionspanspan-idddinstallsoftwaresettingssectionspanddinstallsoftwaresettings-section"></a><span id="DDInstall.SoftwareSettings_Section"></span><span id="ddinstall.softwaresettings_section"></span><span id="DDINSTALL.SOFTWARESETTINGS_SECTION"></span>DDInstall.SoftwareSettings セクション

A *DDInstall*.**SoftwareSettings**セクションが含まれています、 [ **AddReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)ディレクティブや、 [**して**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)ディレクティブ。 各ディレクティブは、レジストリ エントリを追加または削除するためにインストーラーを含む別のライター定義の INF セクションを指します。

たとえば、次のコードは、 **AddReg**という名前のライター定義のレジストリの追加セクションを指すディレクティブ**ACME 1234\_SoftwareDeviceSettings**します。 **して**ディレクティブがという名前の削除レジストリ セクションを指す**ACME 1234\_DeleteSWSettings**します。

```inf
[ACME-1234.SoftwareSettings]
AddReg=ACME-1234_SoftwareDeviceSettings
DelReg=ACME-1234_DeleteSWSettings
```

追加レジストリ セクションでは、4 つのエントリをレジストリに追加し、次のコードに示すように、その値を設定します。

```inf
[ACME-1234_SoftwareDeviceSettings]
HKR,, InstalledDisplayDrivers, %REG_MULTI_SZ%, Acme1
HKR,, OverRideMonitorPower, %REG_DWORD%, 0
HKR,, MultiFunctionSupported, %REG_DWORD%, 1
HKR,, VideoDebugLevel, %REG_DWORD%, 2
```

上記のコードは最初の値を設定、 **InstalledDisplayDrivers**ディスプレイ ドライバーの名前を入力します。 コードの値を設定し、 **OverRideMonitorPower**エントリを 0 に (つまり、 **FALSE**)。 このエントリは、OEM システム ベンダーによってのみ使用する必要があります (たとえば、LCD、CRT、またはテレビ) モニター デバイスの電源の動作を制御します。 1 に設定すると**OverRideMonitorPower** D0 を D3 モニターのデバイスの電力状態を制限します。

3 番目に、コードがの値を設定、 **MultiFunctionSupported**エントリを 1 に (つまり、 **TRUE**)、これは、必要な値は複数の PCI 関数をサポートするアダプターの。 最後の値の設定、コード、 **VideoDebugLevel**エントリで、デバッグ メッセージのビルドの使用をチェックするグローバル デバッグ レベルを制御します。 この値の範囲は 0 (デバッグ メッセージはありません) 3 (最も詳細なメッセージ) ~ です。 グローバル デバッグ レベルの詳細については、次を参照してください。 [ **VideoDebugPrint**](https://docs.microsoft.com/previous-versions/ff570170(v=vs.85))します。

ほとんどのビデオのミニポート ドライバー VGA と互換性がないと、no を必要と**VgaCompatible**レジストリのエントリ。 ビデオのミニポート ドライバーが VGA と互換性のある場合は追加、 **VgaCompatible**エントリをレジストリにその値を 1 に設定 (**TRUE**) 追加レジストリ セクションが表示され、次に示すように。

```registry
[ACME-1234_SoftwareDeviceSettings]
HKR,, VgaCompatible, %REG_DWORD%, 1
```

VGA と互換性のあるビデオのミニポート ドライバーの詳細については、次を参照してください。 [VGA と互換性のあるビデオのミニポート ドライバー (Windows 2000 モデル)](vga-compatible-video-miniport-drivers--windows-2000-model-.md)します。

Delete レジストリの次のセクションでは、次の 3 つのレジストリ エントリを削除します。**GraphicsClocking**、 **MemClocking**、および**CapabilityOverride**します。

```inf
[ACME-1234_DeleteSWSettings]
HKR,, GraphicsClocking
HKR,, MemClocking
HKR,, CapabilityOverride
```

**CapabilityOverride**エントリをシステムは、ディスプレイ ドライバーを無効にする機能を指定します。 たとえば、ディスプレイ ドライバーが実装されている場合でも、 [ **DrvEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)関数 0x10 フラグが設定されている場合に機能を使用できないこと、 **CapabilityOverride**エントリ。

値、 **CapabilityOverride**レジストリ エントリは、次の表に記載されているフラグの 1 つ以上のビット演算 OR。

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
<td align="left"><p>すべてのハードウェア アクセラレータを無効にします。 ハードウェア アクセラレータ スライド バーを移動するのと同じです (で、<strong>表示</strong>コントロール パネルの項目) の最小値設定をします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Microsoft DirectDraw とマイクロソフトの Direct3D ハードウェア アクセラレータのサポートを無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>Direct3D ハードウェア アクセラレータのサポートを無効にします。 呼び出しを防止<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"> <strong>DdGetDriverInfo</strong></a><em>、</em>ドライバーに到達できない Direct3D とコールバックの機能については、どの要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>OpenGL インストール可能なクライアント ドライバー (ICD) と miniclient ドライバー (MCD) のすべてのサポートを無効にします。 呼び出しを防止<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"> <strong>DrvSetPixelFormat</strong></a>、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"> <strong>DrvDescribePixelFormat</strong></a>、および<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)"> <strong>DrvSwapBuffers</strong> </a>ドライバーに到達します。 また、ドライバーに到達できない OPENGL_GETINFO、OPENGL_CMD および MCDFUNCS のエスケープを防止します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>ドライバーのすべてのエスケープのサポートを無効にします。 呼び出しを防止<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)"> <strong>DrvEscape</strong> </a>と<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)"> <strong>DrvDrawEscape</strong> </a>ドライバーに到達します。</p></td>
</tr>
</tbody>
</table>

 

、Windows に同梱されているディスプレイ ドライバーの**CapabilityOverride**は通常 0x8、OpenGL を無効にするに設定します。 OpenGL を無効にする 0x10 フラグを設定する必要はありません、すべてのエスケープを無効にする場合を除き、0x10 フラグを設定する必要がありますに注意してください。

Microsoft Windows XP およびそれ以前のオペレーティング システムを削除しないでください、 **CapabilityOverride**ディスプレイ ドライバーが更新されたときに--などによって提供される最新のドライバーを Windows に含まれるドライバーからのレジストリ エントリを独立系ハードウェア ベンダー (IHV)。 永続的な**CapabilityOverride**エントリ、更新されたドライバに古いドライバーを無効にするのと同じ機能を無効になります。 したがって、Windows XP 用と以前では、次のとおり、**して**既存を明示的に削除する INF ファイルでディレクティブ**CapabilityOverride**エントリ。 Windows XP SP1 と以降のオペレーティング システムを自動的に削除、 **CapabilityOverride**エントリ、これらのシステムは、のでいないを削除するために必要なドライバーが更新されたときに、 **CapabilityOverride**エントリ。

### <a name="span-iddisablingagptransferratesandsidebandaddressingspanspan-iddisablingagptransferratesandsidebandaddressingspanspan-iddisablingagptransferratesandsidebandaddressingspandisabling-agp-transfer-rates-and-sideband-addressing"></a><span id="Disabling_AGP_Transfer_Rates_and_Sideband_Addressing"></span><span id="disabling_agp_transfer_rates_and_sideband_addressing"></span><span id="DISABLING_AGP_TRANSFER_RATES_AND_SIDEBAND_ADDRESSING"></span>AGP 転送の料金と側波帯がアドレス指定を無効にします。

必要に応じて、特定の転送率を AGP または側波帯がアドレス指定を無効にするディスプレイ アダプターの INF ファイルを変更できます。 呼び出すときに、ミニポート ドライバーが AGP 転送速度を変更できることに注意してください[ **AgpSetRate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_set_rate)がこのような呼び出しは、INF ファイルで無効になっている転送速度を変更するのには使用できません。

*Regstr.h*ヘッダー ファイルは、Windows Driver Kit (WDK) に付属している、次のフラグのセットを定義します。

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
<td align="left"><p>1 つの速度 (MHz 66) の転送速度を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_2X_RATE</p></td>
<td align="left"><p>0x00000002L</p></td>
<td align="left"><p>2 回、1 つ速度転送率を無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_4X_RATE</p></td>
<td align="left"><p>0x00000004L</p></td>
<td align="left"><p>4 回、1 つ速度転送率を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AGP_FLAG_NO_8X_RATE</p></td>
<td align="left"><p>0x00000008L</p></td>
<td align="left"><p>8 回、1 つ速度転送率を無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AGP_FLAG_NO_SBA_ENABLE</p></td>
<td align="left"><p>0x00000100L</p></td>
<td align="left"><p>(SBA) のアドレス指定側波帯を無効にします。</p></td>
</tr>
</tbody>
</table>

 

設定の 2 つの種類があります。 グローバルとプラットフォーム固有です。 レジストリには、次の場所にグローバル エントリが含まれています。

```registry
HKLM,"SYSTEM\CurrentControlSet\Control\AGP"
```

フィルター ドライバー サービス キーでは、"Parameters"の下にあるプラットフォーム固有のエントリが見つかります。 たとえば、これらのエントリは、レジストリの次の場所で仮定 AcmeAGP アダプターが存在します。

```registry
HKLM,"SYSTEM\CurrentControlSet\Services\AcmeAGP\Parameters"
```

持つ 0x012A (Nuclear3D) の DeviceID、VendorID 0x1AD0 のテクノロジを使用してプラットフォームでデバイスのアドレス指定側波帯を無効にするには追加、 **Nuclear3D\_Install.HW** INF ファイルにセクション。 (この種類のインストールの INF セクションの詳細については、次を参照してください[ **INF DDInstall.HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。)。このセクションでは、 [ **AddReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)ディレクティブは、次のようにします。

```inf
[Nuclear3D_Install.HW] 
AddReg = Nuclear3D_Reg 
```

次に、次を作成するセクション、 **AddReg**ディレクティブが指します。

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
```

上記のエントリは、HKEY の下のレジストリに追加する HKLM に続く文字列で識別されるサブキーがあることを示します\_ローカル\_マシン ルート。 "1AD0012A"文字列は、エントリ名、元の最初の 4 つの文字は、DeviceID を作成し、最後の 4 つは、この部分の VendorID を作成します。 エントリ名に続く 16 進数のエントリのデータ型を示すフラグのセットで構成されます。 最後の部分は、側波帯がアドレス指定を無効にするエントリの値です。

**重要な**   AGP の逆の順序では、値のエントリでバイト\_フラグ\_いいえ\_SBA\_上記の表に、フラグの定義を有効にします。

 

たとえば、AGP 4 X がこの同じデバイスのすべてのチップセットで区切られていることを確認します。 この事実を示すために 2 番目のエントリを追加、Nuclear3D に\_Reg セクション。

```inf
[Nuclear3D_Reg] 
HKLM,"SYSTEM\CurrentControlSet\Services\viaagp\Parameters","1AD0012A",0x00030003,00,01,00,00,00,00,00,00 
HKLM,"SYSTEM\CurrentControlSet\Control\AGP","1AD0012A",0x00030003,04,00,00,00,00,00,00,00 
```

上記のコードでは、2 番目のエントリは、HKEY の下のレジストリに追加する HKLM に続く文字列で識別されるサブキーがあることを示します\_ローカル\_マシン ルート。 前のエントリのように、このサブキーに関連付けられている値の名前は、デバイスの DeviceID、VendorID で構成される文字列です。 フラグの値も同じです。 値のエントリが AGP\_フラグ\_いいえ\_4 X\_レートで、転送速度 X AGP 4 を無効にします。 前に、この値のエントリ内のバイトが上記の表に、フラグの値の逆の順序では、いることを確認します。

 

 





