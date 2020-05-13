---
title: コンポーネント INF ファイルの使用
description: ソフトウェアコンポーネントを使用して、デバイスに固有のユーザーモードソフトウェアを組み込む方法について説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1aa780491548e6c4859166faefed37b19f3085aa
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235396"
---
# <a name="using-a-component-inf-file"></a>コンポーネント INF ファイルの使用

Windows 10 のデバイスで使用するユーザーモードソフトウェアを含める場合は、次のオプションを使用して[Dch 準拠のドライバー](../develop/getting-started-with-windows-drivers.md)を作成できます。
    
|メソッド|シナリオ|
|---|---|
|[ハードウェアサポートアプリ (HSA)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md) | Microsoft Store から配信および提供される UWP アプリとしてパッケージ化されたデバイスアドオンソフトウェア。  推奨される方法。 |
|ソフトウェア コンポーネント|デバイスアドオンソフトウェアは、MSI または EXE バイナリ、Win32 サービス、または AddReg と CopyFiles を使用してインストールされたソフトウェアです。  参照されるバイナリは、デスクトップのエディション (Home、Pro、および Enterprise) でのみ実行されます。  参照されるバイナリは Windows 10 では実行されません。|

ソフトウェアコンポーネントは、1つまたは複数のソフトウェアモジュールをインストールできる独立したスタンドアロンのドライバーパッケージです。  インストールされているソフトウェアはデバイスの価値を高めますが、基本的なデバイス機能には必要ありません。また、関連付けられた関数ドライバーサービスは必要ありません。  

このページでは、ソフトウェアコンポーネントの使用に関するガイドラインを示します。

## <a name="getting-started"></a>作業の開始

コンポーネントを作成するために、[拡張機能の inf ファイル](using-an-extension-inf-file.md)で Inf [ddinstall ディレクティブ](inf-addcomponent-directive.md)が1回以上指定されています[。](inf-ddinstall-components-section.md)  拡張機能の INF ファイルで参照される各ソフトウェアコンポーネントについて、仮想ソフトウェアで列挙される子デバイスが作成されます。  複数のドライバーパッケージが同じソフトウェアコンポーネントを参照できます。 

仮想デバイスの子は、親デバイスが起動されている限り、他のデバイスと同様に個別に更新できます。  サービスの観点からわかるように、機能をさまざまなグループに分け、グループごとに1つのソフトウェアコンポーネントを作成することをお勧めします。

各ソフトウェアコンポーネントの INF ファイルを提供します。

ソフトウェアコンポーネント INF で[ **addsoftware**ディレクティブ](inf-addsoftware-directive.md)が指定されている場合、コンポーネント inf は次のようになります。

* は、[ユニバーサル INF ファイル](../install/using-a-universal-inf-file.md)である必要があります。
* **ソフトウェアコンポーネント**のセットアップクラスを指定する必要があります。

[ **Addsoftware**ディレクティブ](inf-addsoftware-directive.md)は1回以上指定できます。

>[!NOTE]
>AddSoftware ディレクティブの Type 2 を使用する場合、コンポーネントの INF を利用する必要はありません。  ディレクティブは、どの INF でも正常に使用できます。  ただし、型1の AddSoftware ディレクティブは、コンポーネント INF から使用する必要があります。

また、ソフトウェアコンポーネントデバイスでのすべての INF (コンポーネントまたは not) の照合:

* [Addservice ディレクティブ](inf-addservice-directive.md)を使用して、Win32 ユーザーサービスを指定できます。
* [Inf AddReg ディレクティブ](inf-addreg-directive.md)および[inf CopyFiles ディレクティブ](inf-copyfiles-directive.md)を使用してソフトウェアをインストールできます。
* 関数ドライバーサービスは必要ありません。
* 親デバイスとは別に、ユーザーがアンインストールできます。

コンポーネント INF の例については、「[ドライバーパッケージインストールツールキット (ユニバーサルドライバー用](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU))」を参照してください。

**注**: ソフトウェアで列挙されたコンポーネントデバイスを機能させるには、その親が開始されている必要があります。 親デバイスに使用できるドライバーがない場合、ドライバー開発者は独自のドライバーを作成できます。また、必要に応じて、パススルードライバー "umpass .sys" を利用することもできます。 このドライバーは Windows に含まれており、実質的には、デバイスを起動する以外には何も行いません。 Umpass を使用するには、次に示すように、使用可能な各 [DDInstall.] セクションの [ [ddinstall](inf-ddinstall-section.md) .] セクションで、必要に \* 応じて、該当する [umpass.] セクションに、該当するセクションのいずれかの \* ディレクティブが指定されているかどうかに関係なく、インクルード/ニーズ inf ディレクティブを使用します。

```cpp
[DDInstall]
Include=umpass.inf
Needs=UmPass
; also include any existing DDInstall directives

[DDInstall.HW]
Include=umpass.inf
Needs=UmPass.HW
; also include any existing DDInstall.HW directives

[DDInstall.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces
; also include any existing DDInstall.Interfaces directives

[DDInstall.Services]
Include=umpass.inf
Needs=UmPass.Services
; also include any existing any DDInstall.Services directives
```

## <a name="accessing-a-device-from-a-software-component"></a>ソフトウェアコンポーネントからのデバイスへのアクセス

ソフトウェアコンポーネントに関連付けられているデバイスのデバイスインスタンス ID を取得するには、[ [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)] セクションの [software **arguments** ] 値を、ランタイムコンテキスト変数と共に使用し `<<DeviceInstanceID>>` ます。

その後、実行可能ファイルは、入力された引数リストからソフトウェアコンポーネントのデバイスインスタンス ID を取得できます。  

次に、ソフトウェアコンポーネントがユニバーサル[ターゲットプラットフォーム](../develop/target-platforms.md)を対象としている場合は、次の手順を実行します。

1. デバイスハンドルを取得するには、ソフトウェアコンポーネントのデバイスインスタンス ID を使用して[**CM_Locate_DevNode**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_locate_devnodea)を呼び出します。
2. [**CM_Get_Parent**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)を呼び出して、そのデバイスの親へのハンドルを取得します。  この親は、 [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)を使用してソフトウェアコンポーネントを追加したデバイスです。
3. 次に、親のデバイスインスタンス ID を取得するには、 [**CM_Get_Parent**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)からのハンドルで[**CM_Get_Device_ID**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)を呼び出します。

ソフトウェアコンポーネントがデスクトップ[ターゲットプラットフォーム](../develop/target-platforms.md)のみを対象としている場合は、次の手順を使用します。

1. [**Setupdicreatedeviceinを**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)呼び出して、空のデバイス情報セットを作成します。
2. ソフトウェアコンポーネントデバイスのデバイスインスタンス ID を使用して[**SetupDiOpenDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)を呼び出します。
3. を使用して[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出し、 `DEVPKEY_Device_Parent` 親のデバイスインスタンス ID を取得します。

## <a name="example"></a>例

次の例は、ソフトウェアコンポーネントを使用して、グラフィックスカードの実行可能ファイルを使用してコントロールパネルをインストールする方法を示しています。

### <a name="driver-package-inf-file"></a>ドライバーパッケージ INF ファイル

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
Provider    = %CONTOSO%
DriverVer   = 06/21/2006,1.0.0.0
CatalogFile = ContosoGrfx.cat

[Manufacturer]
%CONTOSO%=Contoso,NTx86

[Contoso.NTx86]
%ContosoGrfx.DeviceDesc%=ContosoGrfx, PCI\VEN0001&DEV0001

[ContosoGrfx.NT]
;empty

[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,, Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001

[Strings]
CONTOSO = "Contoso Inc."
ContosoGrfx.DeviceDesc = "Contoso Graphics Card Extension"
```

### <a name="software-component-inf-file"></a>ソフトウェアコンポーネントの INF ファイル

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = SoftwareComponent
ClassGuid   = {5c4c3332-344d-483c-8739-259e934c9cc8}
Provider    = %CONTOSO%
DriverVer   = 06/21/2006,1.0.0.0
CatalogFile = ContosoCtrlPnl.cat

[SourceDisksNames]
1 = %Disk%,,,""

[SourceDisksFiles]
ContosoCtrlPnl.exe = 1

[DestinationDirs]
DefaultDestDir = 13

[Manufacturer]
%CONTOSO%=Contoso,NTx86

[Contoso.NTx86]
%ContosoCtrlPnl.DeviceDesc%=ContosoCtrlPnl, SWC\VID0001&PID0001&SID0001

[ContosoCtrlPnl.NT]
CopyFiles=ContosoCtrlPnl.NT.Copy

[ContosoCtrlPnl.NT.Copy]
ContosoCtrlPnl.exe

[ContosoCtrlPNl.NT.Services]
AddService = , %SPSVCINST_ASSOCSERVICE%

[ContosoCtrlPnl.NT.Software]
AddSoftware = ContosoGrfx1CtrlPnl,, Software_Inst

[Software_Inst]
SoftwareType = 1
SoftwareBinary = %13%\ContosoCtrlPnl.exe
SoftwareArguments = <<DeviceInstanceID>>
SoftwareVersion = 1.0.0.0

[Strings]
SPSVCINST_ASSOCSERVICE = 0x00000002
CONTOSO = "Contoso"
ContosoCtrlPnl.DeviceDesc = "Contoso Control Panel" 
```

ドライバーの検証と送信のプロセスは、通常の Inf の場合と同じように、コンポーネントの Inf と同じです。 詳細については、「 [WINDOWS HLK はじめに](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)」を参照してください。

セットアップクラスの詳細については、「[ベンダーが使用できるシステム定義のデバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors)」を参照してください。

## <a name="see-also"></a>参照

[INF AddComponent ディレクティブ](inf-addcomponent-directive.md)

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)

[INF DDInstall.Components セクション](inf-ddinstall-components-section.md)

[INF DDInstall.Software セクション](inf-ddinstall-software-section.md)
