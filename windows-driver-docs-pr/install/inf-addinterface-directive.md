---
title: INF AddInterface ディレクティブ
description: 1 つまたは複数の AddInterface ディレクティブは、INF DDInstall.Interfaces セクション内で指定できます。
ms.assetid: 9bd3e051-51f9-4624-802b-b841b25d6616
keywords:
- INF AddInterface ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddInterface Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9edcdba0c1ee776f8613b3c151f6b79337957ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385923"
---
# <a name="inf-addinterface-directive"></a>INF AddInterface ディレクティブ


1 つまたは複数**AddInterface**内でディレクティブを指定することができます、 [ **INF DDInstall.Interfaces セクション**](inf-ddinstall-interfaces-section.md)します。 このディレクティブは、のデバイスに固有のサポートをインストール[デバイス インターフェイス クラス](device-interface-classes.md)他のドライバーやアプリケーションより高いレベルのコンポーネントにエクスポートします。 ディレクティブは通常、参照、*追加インターフェイス セクション*デバイスのインターフェイス クラスのデバイスに固有のインスタンスのレジストリ情報を設定します。

```ini
[DDInstall.Interfaces]
  
AddInterface={InterfaceClassGUID} [,[reference-string] [,[add-interface-section][,flags]]] 
```

エクスポートされたデバイスのインターフェイス クラスは、カーネルがストリーミングでは定義されているなど、デバイスのシステム定義のインターフェイス クラスのいずれかを指定できますかで指定された新しいデバイスのインターフェイス クラス、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md).

## <a name="entries"></a>エントリ


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
デバイスのインターフェイス クラスを識別する GUID 値を指定します。 これは、フォームの明示的な GUID 値として表現できます **{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnnnnnn</em> **}** または % として*strkey*% トークン定義されている **"{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnnnnnn</em> **}"** で、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

GUID を作成する方法の詳細については、次を参照してください。[ドライバーを使用して Guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)します。 システム定義のインターフェイス クラスの GUID など、適切なヘッダーを参照してください*Ks.h*カーネル ストリーミング インターフェイスの Guid。

<a href="" id="reference-string"></a>*参照文字列*  
この省略可能な値は、指定されたインターフェイス クラスのデバイスに固有のインスタンスに関連付けられたを表現できるいずれかを **"** <em>文字列を引用符で囲まれた</em> **"** または %として*strkey*% のトークンで定義されている、 [ **INF 文字列セクション**](inf-strings-section.md)します。

PnP ドライバーの関数とフィルターからこの値を省略は、通常、 **AddInterface =** INF ファイル内のエントリ。 A*参照文字列*を使って、 *swenum*ドライバーには 1 つのインターフェイス クラスの複数のインスタンスを使用してオンデマンドで作成されたソフトウェアのデバイスのプレース ホルダーとして。 同じ*InterfaceClassGUID*値は、2 つの INF エントリで指定されているまたは複数の固有*参照文字列*秒。 I/O マネージャーに渡されるから、*参照文字列*開かれるたびに、インターフェイス インスタンスの名前のパス コンポーネントとして値を 1 つの同じクラスのインターフェイスのインスタンス間でインストールされているドライバーを識別できます。デバイスです。

<a href="" id="add-interface-section"></a>*追加インターフェイス セクション*  
INF ファイルの別の場所のセクションの名前を参照します。 これが通常含まれています、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)このドライバーのサポートをエクスポートするレジストリ エントリを設定する[デバイス インターフェイス クラス](device-interface-classes.md)します。 詳細については、次を参照してください。**解説**セクション。

<a href="" id="flags"></a>*フラグ*  
指定すると、このエントリがゼロにあります。

<a name="remarks"></a>注釈
-------

場合、[デバイス インターフェイス クラス](device-interface-classes.md)によって指定された識別 **{** <em>InterfaceClassGUID</em> **}** がインストールされていなければ、システムのセットアップコードでは、そのクラスをシステムにインストールします。 新しいクラスをインストールする任意の INF ファイルがあります、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)します。 このセクションが含まれていますが、指定した **{** <em>InterfaceClassGUID</em> **}** 参照と、*インターフェイス-section インストール*を設定します。そのクラスのインターフェイスに固有のインストールの操作。

高いレベルのコンポーネントによって実行時の使用のデバイスのインターフェイス クラスのインスタンスを有効にするデバイス ドライバーは呼び出す必要がありますまず[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)のシンボリック リンクの名前を取得します有効にするデバイス インターフェイスのインスタンス。  PnP 関数またはフィルター ドライバーからのこの呼び出しは、通常は、その[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。  デバイス ドライバーを提供する必要があります、INF でプロビジョニングされたデバイスのインターフェイスのインスタンスを有効にする、 **{** <em>InterfaceClassGUID</em> **}** と*参照文字列*を呼び出すときに、INF で指定された[ **IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)します。  ドライバーを呼び出して[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)によって返されるシンボリック リンクの名前を使用してインターフェイスを有効にする[ **IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface). 

各**AddInterface**ディレクティブで、 [ **INF DDInstall.Interfaces セクション**](inf-ddinstall-interfaces-section.md) 、INF ライターの定義を参照できる*追加-インターフェイスのセクション* INF ファイルで別の場所。 各 INF ライター定義セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

*追加インターフェイス セクション*によって参照される、 **AddInterface**ディレクティブは、次の形式。

```ini
[add-interface-section]
 
AddReg=add-registry-section[, add-registry-section]...
[AddProperty=add-property-section[, add-property-section] ...]  (Windows Vista and later versions of Windows)
[DelReg=del-registry-section[, del-registry-section] ...]
[DelProperty=del-property-section[, del-property-section] ...]  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section] ...]
[CopyFiles=@filename | file-list-section[,file-list-section]...]
[DelFiles=file-list-section[,file-list-section]...]
[RenFiles=file-list-section[,file-list-section]...]
[UpdateInis=update-ini-section[, update-ini-section] ...]
[UpdateIniFields=update-inifields-section[, update-inifields-section] ...]
[Ini2Reg=ini-to-registry-section[, ini-to-registry-section] ...]
```

Windows Vista 以降、プロパティを設定できますデバイス インターフェイスを含めることによって[ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md) add インターフェイスのセクションでします。 含めることによって、デバイス インターフェイスのプロパティを削除することも[ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)で、*追加 interface セクション*します。 ただし、使用する必要があります**AddProperty**または**DelProperty**ディレクティブは、Windows Vista または Windows オペレーティング システムの以降のバージョンに新しいデバイス インターフェイスのプロパティを変更するだけです。 デバイス インターフェイス プロパティの Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ値のエントリがある場合は、使用する続行する必要があります[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)を設定し、デバイス インターフェイスのプロパティを削除します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。 使用する方法についての詳細、 **AddProperty**ディレクティブと**DelProperty**ディレクティブを参照してください[INF AddProperty ディレクティブとINFDelPropertyディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md).

通常、*追加インターフェイス セクション*のみが含まれています、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md) 、1 つをさらに、参照するには、*追加-レジストリ-セクション*. *追加レジストリ セクション*も高いレベルのドライバーとアプリケーションでデバイス ドライバーを後で使用でサポートされているインターフェイスのレジストリに情報を格納するために使用します。

*追加レジストリ セクション*内で参照されている、*追加インターフェイス セクション*デバイス、ドライバー、およびインターフェイスのインスタンスに固有です。 ユーザー インターフェイスで、フレンドリ名でそのインターフェイスにも高いレベルのコンポーネントが参照できるように、エクスポートされたデバイスのインターフェイスのインスタンスのフレンドリ名を定義する値のエントリがあります。

**HKR**などで指定された、*追加レジストリ セクション*セクションは、デバイス インターフェイスの実行時アクセス可能な状態のレジストリ キーを指定します。  ドライバーは呼び出すことによって、実行時にこのレジストリ キーに格納されている状態でアクセスできる[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)状態のレジストリ キーを識別するハンドルを取得します。  ユーザー モード コンポーネントは、呼び出すことによって、状態を照会できます[ **CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)します。

<a name="examples"></a>例
--------

この例では一部の拡張、 *DDInstall*.**インターフェイス**システム定義のカーネル ストリーミング インターフェイスをサポートする特定のオーディオ デバイスのセクション。

```ini
; ...
[ESS6881.Device.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,\
ESSAud.Interface.Topology
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_FMSynth%,WDM.Interface.FMSynth
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_FMSynth%,\
WDM.Interface.FMSynth

[ESSAud.Interface.Wave]
AddReg=ESSAud.Interface.Wave.AddReg

[ESSAud.Interface.Wave.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%ESSAud.Wave.szPname%
; ... 
[WDM.Interface.UART]
AddReg=WDM.Interface.UART.AddReg

[WDM.Interface.UART.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%WDM.UART.szPname%
; ...
[Strings]
KSCATEGORY_AUDIO="{6994ad04-93ef-11d0-a3cc-00a0c9223196}"
KSCATEGORY_RENDER="{65e8773e-8f56-11d0-a3b9-00a0c9223196}"
KSCATEGORY_CAPTURE="{65e8773d-8f56-11d0-a3b9-00a0c9223196}"
; ...
KSNAME_WAVE="Wave"
KSNAME_UART="UART"
; ...
Proxy.CLSID="{17cca71b-ecd7-11d0-b908-00a0c9223196}"
; ... 
ESSAud.Wave.szPname="ESS AudioDrive" 
; ... 
```

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






