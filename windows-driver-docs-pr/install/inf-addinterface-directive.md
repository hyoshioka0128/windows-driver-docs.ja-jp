---
title: INF AddInterface ディレクティブ
description: 1つまたは複数の AddInterface ディレクティブは、INF DDInstall. Interface セクション内で指定できます。
ms.assetid: 9bd3e051-51f9-4624-802b-b841b25d6616
keywords:
- INF AddInterface ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddInterface Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecef85a4d1dac6a692f107019710cac26c603d4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828804"
---
# <a name="inf-addinterface-directive"></a>INF AddInterface ディレクティブ


1つまたは複数の**Addinterface**ディレクティブは、 [**INF Ddinstall. interface セクション**](inf-ddinstall-interfaces-section.md)内で指定できます。 このディレクティブは、他のドライバーやアプリケーションなどの上位レベルのコンポーネントにエクスポートされた[デバイスインターフェイスクラス](device-interface-classes.md)のデバイス固有のサポートをインストールします。 このディレクティブは、通常、デバイスインターフェイスクラスのデバイス固有のインスタンスのレジストリ情報を設定する、*インターフェイスの追加セクション*を参照します。

```ini
[DDInstall.Interfaces]
  
AddInterface={InterfaceClassGUID} [,[reference-string] [,[add-interface-section][,flags]]] 
```

エクスポートされたデバイスインターフェイスクラスは、システム定義のデバイスインターフェイスクラス (カーネルストリーミングによって定義されているものなど)、または[**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)で指定された新しいデバイスインターフェイスクラスのいずれかになります。

## <a name="entries"></a>エントリ


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
デバイスインターフェイスクラスを識別する GUID 値を指定します。 これは、 **{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn</em> **}** または%*strkey*% トークンの形式の明示的な GUID 値として表すことができます。INF ファイルの[**文字列**](inf-strings-section.md)セクションで **"{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn</em> **}"** に定義されています。

GUID を作成する方法の詳細については、「[ドライバーでの guid の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)」を参照してください。 システム定義のインターフェイスクラス GUID については、カーネルストリームインターフェイス Guid の*Ks*など、適切なヘッダーを参照してください。

<a href="" id="reference-string"></a>*参照-文字列*  
この省略可能な値は、指定されたインターフェイスクラスのデバイス固有のインスタンスに関連付けられており、 **"** <em>引用符で囲まれた文字列</em> **"** として、または[**INF 文字列セクション**](inf-strings-section.md)で定義されている%*strkey*% token として表すことができます。

PnP 関数とフィルタードライバーは通常、その INF ファイルの**Addinterface =** エントリからこの値を除外します。 *参照文字列*は、単一のインターフェイスクラスの複数のインスタンスを使用して、オンデマンドで作成されるソフトウェアデバイスのプレースホルダーとして*swenum*ドライバーによって使用されます。 同じ*InterfaceClassGUID*値は、2つ以上の一意の*参照文字列*s を持つ INF エントリで指定できます。 I/o マネージャーは、*参照文字列*の値を、インターフェイスインスタンスの名前のパスコンポーネントとして開いたときに常に渡します。そのため、インストールされているドライバーは、1つのデバイスに対して同じクラスのインターフェイスインスタンスを識別できます。

<a href="" id="add-interface-section"></a>*インターフェイスの追加-セクション*  
INF ファイル内の別の場所にあるセクションの名前を参照します。 これには通常、この[デバイスインターフェイスクラス](device-interface-classes.md)のドライバーのサポートをエクスポートするレジストリエントリを設定するための[**INF AddReg ディレクティブ**](inf-addreg-directive.md)が含まれています。 詳細については、次の「**解説**」を参照してください。

<a href="" id="flags"></a>*示す*  
指定する場合、このエントリは0である必要があります。

<a name="remarks"></a>注釈
-------

指定した **{** <em>InterfaceClassGUID</em> **}** によって識別される[デバイスインターフェイスクラス](device-interface-classes.md)がまだインストールされていない場合は、システムセットアップコードによってそのクラスがシステムにインストールされます。 新しいクラスをインストールするすべての INF ファイルには、 [**Inf InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)もあります。 このセクションには、指定した **{** <em>InterfaceClassGUID</em> **}** が含まれており、そのクラスのインターフェイス固有のインストール操作を設定する*インターフェイスのインストールセクション*が参照されています。

上位レベルのコンポーネントが実行時に使用するデバイスインターフェイスクラスのインスタンスを有効にするには、デバイスドライバーが[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出して、有効にするデバイスインターフェイスインスタンスのシンボリックリンク名を取得する必要があります。  通常、PnP 関数またはフィルタードライバーは、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからこの呼び出しを行います。  Inf でプロビジョニングされたデバイスインターフェイスのインスタンスを有効にするには、デバイスドライバーが[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出すときに、inf に指定されている **{** <em>InterfaceClassGUID</em> **}** と*参照文字列*を提供する必要があります。  次に、ドライバーは[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出して、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)によって返されたシンボリックリンク名を使用してインターフェイスを有効にします。 

Inf [**DDInstall. interface セクション**](inf-ddinstall-interfaces-section.md)の各**addinterface**ディレクティブは、inf ファイル内の別の場所にある inf ライターで定義された*インターフェイスセクション*を参照できます。 各 INF ライターで定義されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**Addinterface**ディレクティブによって参照される*インターフェイスセクション*には、次の形式があります。

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

Windows Vista 以降では、[インターフェイスの追加] セクションで[**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)を含めることによって、デバイスインターフェイスのプロパティを設定できます。 また、[*インターフェイスの追加] セクション*で[**INF delproperty ディレクティブ**](inf-delproperty-directive.md)を含めることによって、デバイスインターフェイスのプロパティを削除することもできます。 ただし、 **addproperty**ディレクティブまたは**delproperty**ディレクティブは、windows Vista 以降のバージョンの windows オペレーティングシステムの新しいデバイスインターフェイスプロパティを変更する場合にのみ使用してください。 Windows Server 2003、Windows XP、または Windows 2000 で導入され、対応するレジストリ値のエントリを持つデバイスインターフェイスのプロパティの場合は、 [**Inf AddReg ディレクティブ**](inf-addreg-directive.md)と[**inf delreg ディレクティブ**](inf-delreg-directive.md)を使用して、およびを設定します。デバイスインターフェイスのプロパティを削除します。 これらのガイドラインは、システム定義のプロパティとカスタムプロパティに適用されます。 **Addproperty**ディレクティブおよび**delproperty**ディレクティブの使用方法の詳細については、「 [INF Addproperty ディレクティブと inf delproperty ディレクティブ](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)の使用」を参照してください。

通常、AddReg*は、* 1 つの*レジストリセクション*を参照する INF の[**ディレクティブ**](inf-addreg-directive.md)だけを含んでいます。 *レジストリの追加-セクション*は、デバイスドライバーでサポートされているインターフェイスに関する情報をレジストリに格納するために使用されます。これは、それ以降も上位レベルのドライバーとアプリケーションで使用できます。

*Add-interface*セクション内で参照される*レジストリセクション*は、デバイス、ドライバー、およびインターフェイスのインスタンスに固有です。 エクスポートされたデバイスインターフェイスインスタンスのフレンドリ名を定義する値エントリがある可能性があります。これにより、上位レベルのコンポーネントは、ユーザーインターフェイスのフレンドリ名でそのインターフェイスを参照できます。

このような*add registry*セクションで指定された**hkr**は、デバイスインターフェイスの実行時にアクセス可能な状態のレジストリキーを指定します。  ドライバーは、 [**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)を呼び出して状態レジストリキーへのハンドルを取得することにより、このレジストリキーに格納されている状態にアクセスできます。  ユーザーモードのコンポーネントは、 [**CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)を呼び出すことによって状態を照会できます。

<a name="examples"></a>例
--------

この例では、 *Ddinstall*の展開の一部を示します。システム定義のカーネルストリーミングインターフェイスをサポートする特定のオーディオデバイスの**インターフェイス**セクション。

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

[***Ddinstall *.インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






