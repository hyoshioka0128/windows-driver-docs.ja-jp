---
title: INF DDInstall.HW セクション
description: 通常、DDInstall. HW セクションは、多機能デバイスをインストールするために使用されます。 PnP フィルタードライバーをインストールする場合や、ユーザーがアクセス可能なデバイス固有の情報をレジストリに設定する場合は、明示的な AddReg ディレクティブを使用する場合もインクルードする場合も、エントリが必要な場合もあります。
ms.assetid: 417a4ab0-9723-4b3b-aa8c-342598874d61
keywords:
- INF DDInstall. HW セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.HW Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e08c1925d71c8d3c0bb406cdbe8a15c8c03f4ce9
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223244"
---
# <a name="inf-ddinstallhw-section"></a>INF DDInstall.HW セクション


<em>Ddinstall</em>**。HW**セクションは通常、多機能なデバイスをインストールするために使用されます。 PnP フィルタードライバーをインストールする場合や、ユーザーがアクセスできるデバイス固有の情報をレジストリに設定する場合は、明示的な[**AddReg**](inf-addreg-directive.md)ディレクティブを使用するか、Include エントリと必要条件を**指定**する**必要**があります。

```inf
[install-section-name.HW] |
[install-section-name.nt.HW] |
[install-section-name.ntx86.HW] |
[install-section-name.ntarm.HW] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.HW] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.HW] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.HW]  (Windows XP and later versions of Windows)
 
[AddReg=add-registry-section[,add-registry-section]...] ...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[DelReg=del-registry-section[,del-registry-section]...] ...
[BitReg=bit-registry-section[,bit-registry-section] ...] 
```

## <a name="entries"></a>エントリ


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>registry</em>\[-section **、**<em>add-section</em>\]...  
この<em>Ddinstall</em>によってカバーされるデバイスの inf ファイル内の他の場所で、1つまたは複数の inf ライターで定義された*レジストリセクション*を参照し**ます。HW**セクション。 *レジストリの追加-セクション*では、通常、デバイスごとの情報をレジストリにインストールします。 このような*add registry セクション*の**hkr**仕様では、デバイスの*ハードウェアキー*、デバイスに関する情報を含むデバイス固有のレジストリサブキーが指定されています。 ハードウェアキーは、デバイスキーとも呼ばれます。 詳細については、「[デバイスとドライバーのレジストリツリーとキー](https://docs.microsoft.com/windows-hardware/drivers/install/registry-trees-and-keys)」を参照してください。 ドライバーパッケージは、 **Ddinstall. HW セクション**で参照される [レジストリの追加] セクションで**hkr**仕様を使用して、INF を介して設定を追加できます。 

詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**. .inf**\[**,**<em>filename2</em>**.inf**\]...  
このデバイスのインストールに必要なセクションを含む、システムが提供する追加の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf-name</em>\[**,**<em>inf-name</em>\]...  
このデバイスのインストール中に処理する必要がある名前付きセクションを指定します。 通常、このような名前付きセクションは、 <em>Ddinstall</em>**です。****インクルード**エントリに記載されているシステム提供の INF ファイル内の HW セクション。 ただし、このような<em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。** 含まれている INF の HW セクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**Delreg =**<em>del-registry-section</em>\[**,**<em>del-セクション</em>\]...  
この*Ddinstall*セクションでカバーされているデバイスのドライバーについて、inf ファイル内の他の場所にある1つ以上の inf ライターで定義された*削除セクション*を参照します。 このような削除レジストリセクションは、以前にインストールされたデバイス/ドライバーの古いレジストリ情報を対象のコンピューターから削除します。 このような delete registry セクションの**Hkr**仕様では、 **AddReg**の場合と同じサブキーが指定されています。

このディレクティブはほとんど使用されていません。ただし、この*Ddinstall*セクションの名前を定義している [製造元ごとに製造*単位] セクション*に記載されているものと同じデバイスまたはモデルの以前のインストールをアップグレードする INF ファイルは除きます。 詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

<a href="" id="bitreg-bit-registry-section--bit-registry-section-----"></a>**Bitreg =**<em>ビットレジストリ-セクション</em>\[**、**<em>ビットレジストリ-セクション</em>\] ...  
このセクションでは有効ですが、ほとんど使用されませんでした。 参照されるビットレジストリセクション内の**Hkr**仕様は、 **AddReg**の場合と同じサブキーを指定します。 詳細については、「 [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)」を参照してください。

<a name="remarks"></a>解説
-------

正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような<em>ddinstall</em>に挿入でき**ます。** クロスプラットフォームの INF ファイルの HW セクション名。 システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

任意の<em>Ddinstall</em>**。HW**セクションには、次のいずれかが必要です。

- **AddReg**ディレクティブ。
- 別の INF ファイルを指定する**インクルード**エントリ。 この場合、 <em>Ddinstall がインストール</em>さ**れます。HW**セクションには、他の INF ファイルのセクションを指定する、対応する**必要**なエントリも含まれている必要があります。 このセクションは、必要なレジストリ情報を設定するために使用されます。

<em>Ddinstall</em>の各ディレクティブ **。HW**セクションでは、複数の INF ライターで定義されたセクションを参照できます。 ただし、追加の名前付きセクションは、それぞれコンマ (,) で区切られている必要があります。

各セクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

多機能デバイスのインストール方法の詳細については、「[多機能デバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/multifunction/index)」を参照してください。

<a name="examples"></a>例
--------

この例は、CD-ROM デバイスクラスインストーラーが<em>Ddinstall</em>を使用する方法を示して**います。HW**セクションと<em>ddinstall</em>**。** 適切なレジストリセクションを作成し、それらを PnP 上位フィルタードライバーとして設定することによって、CD オーディオとチェンジャーの両方の機能をサポートするためのサービスセクション。

```inf
;;
;; Installation section for cdaudio. Sets cdrom as the service 
;; and adds cdaudio as a PnP upper filter driver. 
;;
[cdaudio_install]
CopyFiles=cdaudio_copyfiles,cdrom_copyfiles

[cdaudio_install.HW]
AddReg=nosync_addreg,cdaudio_addreg
 ; cdaudio_addreg required to register this as a PnP filter driver

[cdaudio_install.Services]
AddService=cdrom,0x00000002,cdrom_ServiceInstallSection
AddService=cdaudio,,cdaudio_ServiceInstallSection

[changer_install]
CopyFiles=changer_copyfiles,cdrom_copyfiles

[changer_install.HW]
AddReg=changer_addreg

; ... changer_install.Services section similar to cdaudio's

; ... some similar cdrom_install(.HW)/addreg sections omitted 

[cdaudio_addreg] ; changer_addreg section has similar entry
HKR,,"UpperFilters",0x00010000,"cdaudio" ; [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) value 

;
; Use next section to disable synchronous transfers to this device. 
; Sync transfers will always be turned off by default in this INF 
; for any cdrom-type device.
;
[nosync_addreg]
HKR,,"DefaultRequestFlags",0x00010001,8

[autorun_addreg]
HKLM,"System\CurrentControlSet\Services\cdrom","AutoRun",0x00010003,1
;;
;; service-install sections for cdrom, cdaudio, and changer
;;
[cdrom_ServiceInstallSection]
DisplayName    = %cdrom_ServiceDesc%
ServiceType    = 1
StartType      = 1
ErrorControl   = 1
ServiceBinary  = %12%\cdrom.sys
LoadOrderGroup = SCSI CDROM Class
AddReg         = autorun_addreg

[cdaudio_ServiceInstallSection]
DisplayName    = %cdaudio_ServiceDesc%
ServiceType    = 1
StartType      = 1
ErrorControl   = 1
ServiceBinary  = %12%\cdaudio.sys

; ... changer_ServiceInstallSection similar to cdaudio's
```

## <a name="see-also"></a>関連項目


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






