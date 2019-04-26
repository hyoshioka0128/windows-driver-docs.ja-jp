---
title: INF ファイルで、Reflector を指定します。
description: INF ファイルで、Reflector を指定します。
ms.assetid: 3676c99d-4e13-4385-910a-251232b00d4c
keywords:
- リフレクター WDK UMDF
- AddService
- INF ファイル WDK UMDF、リフレクター
- 機能ドライバー WDK UMDF
- フィルター ドライバー WDK UMDF
- リフレクター WDK UMDF の読み込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bec546532b0d656dc3a493e30ff1a7d7dd34c2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350724"
---
# <a name="specifying-the-reflector-in-an-inf-file"></a>INF ファイルで、Reflector を指定します。


Reflector (WUDFRd.sys)、カーネル モード デバイス スタックに追加する UMDF ドライバーの INF ファイルを含める必要があります、 [ **AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)で、 [ **INF DDInstall.Servicesセクション**](https://msdn.microsoft.com/library/windows/hardware/ff547349)します。 Reflector は、上部のフィルター、下位のフィルター、またはユーザー モードのスタックの構成によって、デバイスのサービスを指定できます。

次のコード例では、UMDF 関数ドライバーの INF ファイルが、reflector を追加する方法を示します。

```cpp
[Skeleton_Install.Services]
AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall
```

この例で、ドライバーは、0x2 を指定します (SPSVCINST\_ASSOCSERVICE) フラグ (に入れて、*フラグ*上記のパラメーター)、カーネル モード デバイス スタック内の関数のドライバーとして、reflector を割り当てる。

**AddService**ディレクティブでは、既存のサービス構成が上書きされないように 0x000001f8 フラグもを設定します。 これらのフラグの詳細については、次を参照してください。、*フラグ*のパラメーター、 [ **AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)します。

WUDFVhidmini サンプルでは、次のコード例を示しています、 **AddService** UMDF フィルター ドライバーのディレクティブ。

```cpp
[hidumdf.win8.NT.Services]
AddService=WUDFRd,0x000001f8,WUDFRD_ServiceInstall  
AddService=mshidumdf, 0x000001fa, mshidumdf.AddService

[WudfVhidmini_AddReg]
HKR,,"LowerFilters",0x00010008,"WUDFRd" ; FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
```

ここでは、mshidumdf サービスは、デバイス スタックの FDO を関連付けられ、reflector は、下位のフィルター。

## <a name="providing-a-service-install-section"></a>サービス インストール セクションを提供します。


**AddService**ディレクティブ参照サービスのインストール-セクションを次のコード例に似ています。 **ServiceType** 1 または、0x00000001、INF が 1 つまたは複数のデバイスのサポートをインストールすることを示す、エントリを指定します。 **StartType**エントリでは、ドライバーを開始するタイミングを指定します。 **ErrorControl**エントリは、ドライバーにはエラー制御のレベルを指定します。 **ServiceBinary**エントリは、サービスのバイナリ (reflector) へのパスを指定します。

```cpp
[WUDFRD_ServiceInstall]
DisplayName = "Windows Driver Frameworks - User-mode Driver Framework Reflector"
ServiceType=1
StartType=3
ErrorControl=1
ServiceBinary=%12%\WUDFRd.sys
```

## <a name="specifying-a-unique-service-name"></a>一意のサービス名を指定します。


そのためには必要ありませんが、Windows 8 およびそれ以降のオペレーティング システムでのみ実行される UMDF ドライバーは WUDFRd (reflector) サービスの一意のサービス名を指定できます。

次の例では、WUDFRd ではなく、一意のサービス名を指定する方法を示します。

```cpp
[Echo_Install.NT.Services]
AddService=WudfEchoDriver,0x00000002,WUDFEchoDriver_ServiceInstall

[WUDFEchoDriver_ServiceInstall]
DisplayName = %WudfEchoDriverDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys
StartName = \Driver\WudfRd
```

上記の例では、ドライバーは一意の値では、サービス名を指定します、 **AddService**ディレクティブ。 (この場合は WudfEchoDriver で、ドライバーの名前を指定します。)次に、ドライバーを指定する一意**DisplayName**サービスの値。 最後に、ドライバーを追加、 **StartName**エントリに設定し、\\ドライバー\\WudfRd します。

UMDF ドライバーのオペレーティング システムでは、一意のサービス名、reflector を Windows 8 より前指定できません。 ドライバーが一意のサービス名を指定する必要があります Windows 8 より前動作のオペレーティング システムでも場合は、次の例に示すように、INF ファイルで特定のセクションではオペレーティング システムを使用します。

```cpp
[Manufacturer]
%MSFT% = Microsoft,NTx86.6.0,NTx86.6.2
[Microsoft.NTx86.6.0]
%Sensors.DeviceDesc% = Sensors_Install_VistaWin7,HID_DEVICE_UP:0020_U:0001
[Microsoft.NTx86.6.2]
%Sensors.DeviceDesc% = Sensors_Install_Win8,HID_DEVICE_UP:0020_U:0001
[Sensors_Install_VistaWin7]
--- Install the device this way on Vista/Win7 ---
[Sensors_Install_Win8]
--- Install the device in a different way on Win8 ---
```

リフレクターが追加されない場合は、UMDF は読み込まれていません。 デバイスが開始可能性がありますが、ホスト プロセスが存在しないと、デバイスが正しく動作しません。

 

 





