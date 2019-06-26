---
title: フィルター ドライバーのインストール
description: フィルター ドライバーのインストール
ms.assetid: 48ffa6db-3254-4108-b8bb-5884b9168a9d
keywords:
- デバイス セットアップ WDK デバイスのインストール、フィルター ドライバー
- デバイスのインストール WDK、フィルター ドライバー
- デバイス WDK をインストールするには、フィルター ドライバー
- フィルター ドライバー WDK デバイスのインストール
- デバイス固有のフィルター ドライバー WDK デバイスのインストール
- クラスのフィルター ドライバー WDK デバイスのインストール
- SetupInstallFilesFromInfSection
- 再
- LowerFilters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f8abfbfc3d2a4379bf8ed3c80de2f3db987ed5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379465"
---
# <a name="installing-a-filter-driver"></a>フィルター ドライバーのインストール





PnP フィルター ドライバーは、セットアップ クラスの特定のデバイスやすべてのデバイスをサポートし、デバイスの機能のドライバー (上位のフィルター) の上またはデバイスの機能のドライバー (低いフィルター) の下にアタッチできます。 参照してください[WDM ドライバーの種類](https://docs.microsoft.com/windows-hardware/drivers/kernel/types-of-wdm-drivers)PnP ドライバーのレイヤーの詳細についてはします。

### <a href="" id="ddk-installing-a-device-specific-filter-driver-dg"></a>デバイス固有のフィルター ドライバーをインストールします。

デバイス固有のフィルター ドライバーに登録するでのレジストリ エントリを作成、 **AddReg**内のエントリ、 <em>DDInstall</em>**します。HW**デバイスの INF ファイルのセクション。 特定のデバイス上のフィルターでは、という名前のエントリを作成**再**します。 デバイスに固有の低いフィルターでは、という名前のエントリを作成**LowerFilters**します。 たとえば、INF の抜粋を次のインストール*オーディオ*の上部のフィルターとして、 *cdrom*ドライバー。

```cpp
:
; Installation section for cdaudio. Sets cdrom as the service 
; and adds cdaudio as a PnP upper filter driver. 
;
[cdaudio_install]
CopyFiles=cdaudio_copyfiles, cdrom_copyfiles
 
[cdaudio_install.HW]
AddReg=cdaudio_addreg
 
[cdaudio_install.Services]
AddService=cdrom,0x00000002,cdrom_ServiceInstallSection
AddService=cdaudio,,cdaudio_ServiceInstallSection
: 

[cdaudio_addreg] 
HKR,,"UpperFilters",0x00010000,"cdaudio" ; REG_MULTI_SZ value 
:

[cdaudio_ServiceInstallSection]
DisplayName    = %cdaudio_ServiceDesc%
ServiceType    = 1     ; SERVICE_KERNEL_DRIVER
StartType      = 3     ; SERVICE_DEMAND_START
ErrorControl   = 1     ; SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\cdaudio.sys
:
```

### <a href="" id="ddk-installing-a-class-filter-driver-dg"></a>クラスのフィルター ドライバーをインストールします。

必要なサービスをインストールするには、クラス全体上または下-フィルターのデバイス セットアップ クラスに対するをインストールするには、します。 アプリケーションは、上または下-フィルターの目的のデバイス セットアップ クラスと、サービスを登録できます。 サービス バイナリをコピーするアプリケーションを使用できます**SetupInstallFilesFromInfSection**します。 サービスをインストールするには、アプリケーションを使用できます**SetupInstallServicesFromInfSection**します。 アプリケーションの呼び出しを上または下の特定のデバイス セットアップ クラスに対するフィルターとして、サービスを登録する**SetupInstallFromInfSection**関心のあるデバイス セットアップ クラスごとには、取得したレジストリ キー ハンドルを使用して[ **SetupDiOpenClassRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)の*RelativeKeyRoot*パラメーター。 たとえば、INF セクションでは、次を考慮してください。

```cpp
:

[DestinationDirs]
upperfilter_copyfiles = 12

[upperfilter_inst]
CopyFiles = upperfilter_copyfiles
AddReg = upperfilter_addreg

[upperfilter_copyfiles]
upperfilt.sys,,,0x00004000  ; COPYFLG_IN_USE_RENAME

[upperfilter_addreg]
; append this service to existing REG_MULTI_SZ list, if any
HKR,,"UpperFilters",0x00010008,"upperfilt" 

[upperfilter_inst.Services]
AddService = upperfilt,,upperfilter_service

[upperfilter_service]
DisplayName   = %upperfilter_ServiceDesc%
ServiceType   = 1   ; SERVICE_KERNEL_DRIVER
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 1   ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\upperfilt.sys
:
```

デバイスのインストール アプリケーションは。

1.  呼び出す**SetupInstallFilesFromInfSection**の\[upperfilter_inst\]セクション。

2.  呼び出す**SetupInstallServicesFromInfSection**の\[upperfilter_inst します。サービス\]セクション。

3.  呼び出す**SetupInstallFromInfSection**の\[upperfilter_inst\]セクションで、クラス キーごとに登録すると、 *upperfilt*のサービスです。

各呼び出しは指定**SPINST_REGISTRY**の*フラグ*をレジストリの変更のみを実行する必要があることを示すために、引数。

 

 





