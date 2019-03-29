---
title: INF DDInstall.HW セクション
description: DDInstall.HW のセクションでは通常、PnP フィルター ドライバーをインストールするため、レジストリで、ユーザーがアクセスできる特定のデバイスがドライバーに依存しない情報を設定および多機能デバイスをインストールするかどうかと共に使用明示的な AddRegディレクティブまたは Include およびニーズのエントリを含むです。
ms.assetid: 417a4ab0-9723-4b3b-aa8c-342598874d61
keywords:
- INF DDInstall.HW セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.HW Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23052d536b36ab488c793e9b70ee9fecc019d951
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350173"
---
# <a name="inf-ddinstallhw-section"></a>INF DDInstall.HW セクション


<em>DDInstall</em>**します。HW**のセクションでは通常、PnP フィルター ドライバーをインストールするため、レジストリで、ユーザーがアクセスできる特定のデバイスがドライバーに依存しない情報を設定および多機能デバイスをインストールするかどうかと共に使用明示的な[**AddReg** ](inf-addreg-directive.md)ディレクティブまたは**Include**と**必要がある**エントリ。

```ini
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


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
1 つを参照またはより INF ライター-定義*追加レジストリ セクション*この対象となるデバイスの INF ファイルの他の場所で<em>DDInstall</em>**します。HW**セクション。 *追加レジストリ セクション*通常フィルターのインストールや、レジストリにデバイスごとの情報を格納します。 **HKR**などの仕様、*追加レジストリ セクション*デバイスの指定*ハードウェア キー*、デバイス固有のレジストリ サブキーに関する情報を格納します。デバイスです。 ハードウェア キーは、デバイス キーとも呼ばれます。 詳細については、次を参照してください。[レジストリ ツリーとデバイスとドライバーのキー](https://docs.microsoft.com/windows-hardware/drivers/install/registry-trees-and-keys)します。 ドライバー パッケージを使用して、INF を使用して設定を追加することができます、 **HKR**仕様によって参照の追加-レジストリのセクションでは、 **DDInstall.HW セクション**します。 

詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
1 つまたは複数追加システムが指定した INF ファイルをこのデバイスをインストールするために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
このデバイスのインストール中に処理する必要がある名前付きセクションを指定します。 通常、このような名前付きセクションは、 <em>DDInstall</em>**します。HW**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。HW**の含まれる INF セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
1 つを参照またはより INF ライター-定義*delete-section レジストリ*これで、デバイスのドライバーの INF ファイルで別の場所がカバー *DDInstall*セクション。 このような削除レジストリ セクションでは、対象のコンピューターから以前にインストールしたデバイス/ドライバーの古いレジストリ情報を削除します。 **HKR**仕様 delete レジストリのセクションで指定の場合と同様に、同じサブキー **AddReg**します。

このディレクティブはあまり使われない点を除いて、INF ファイルあたりの製造元ごとに表示されている同じデバイス/モデルの以前のインストールをアップグレード-*モデル*これの名前を定義するセクション*DDInstall*セクション。 詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

<a href="" id="bitreg-bit-registry-section--bit-registry-section-----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\] ...  
このセクションで有効ですが、ほとんどない使用です。 **HKR**仕様が参照されているビット レジストリ セクションでは指定の場合と同様に、同じサブキー **AddReg**します。 詳細については、次を参照してください。 [ **INF BitReg ディレクティブ**](inf-bitreg-directive.md)します。

<a name="remarks"></a>コメント
-------

大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 <em>DDInstall</em>**します。HW**クロスプラット フォーム対応の INF ファイルでセクション名。 詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

すべて<em>DDInstall</em>**します。HW**セクションには、次のいずれかが必要があります。

- **AddReg**ディレクティブ。
- **Include**エントリを別の INF ファイルを指定します。 ここで、 <em>DDInstall</em>**します。HW**セクションでは、対応するを含める必要がありますも**必要があります**エントリをその他の INF ファイルでセクションを指定します。 このセクションでは、必要なレジストリ情報の設定に使用されます。

各ディレクティブを<em>DDInstall</em>**します。HW**セクションは、1 つ以上の INF ライター定義のセクションを参照できます。 ただし、各追加の名前付きセクションは、コンマ (,) で区切る必要があります。

このような各セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

多機能デバイスをインストールする方法の詳細については、次を参照してください。[多機能デバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff542743)します。

<a name="examples"></a>使用例
--------

この例は、CD-ROM デバイス クラスのインストーラーを使用する方法を示しています。 <em>DDInstall</em>**します。HW**セクションと<em>DDInstall</em>**します。サービス**セクションでは PnP としてこれらを上部のフィルター ドライバーの設定を適切なレジストリ セクションを作成して CD オーディオおよびチェンジャー機能の両方をサポートするためにします。

```ini
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

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

 

 






