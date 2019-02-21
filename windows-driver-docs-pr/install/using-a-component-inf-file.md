---
title: コンポーネントの INF ファイルを使用します。
description: ソフトウェア コンポーネントを使用して、デバイスに固有のユーザー モード ソフトウェアを追加する方法について説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 633023f0187a3ff1d331d1bdf83bad258d125ce1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529024"
---
# <a name="using-a-component-inf-file"></a>コンポーネントの INF ファイルを使用します。

Windows 10 デバイスで使用するためのユーザー モード ソフトウェアを含める場合は、作成するには、次のオプションがある、 [DCHU 準拠ユニバーサル ドライバー](../develop/getting-started-with-universal-drivers.md):
    
|メソッド|シナリオ|
|---|---|
|[アプリ (HSA) のハードウェア サポート](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md) | デバイスのアドオン ソフトウェア配信され、Microsoft Store からサービスを提供する UWP アプリとしてパッケージ化します。  推奨される方法です。 |
|ソフトウェア コンポーネント|デバイス アドオン ソフトウェアは、MSI または EXE のバイナリは、Win32 サービス、または AddReg と CopyFiles を使用してインストールされているソフトウェアです。  参照先のバイナリは、デスクトップのエディション (Home、Pro、および Enterprise) でのみ実行されます。  参照先のバイナリは、Windows 10 では実行されません。|

ソフトウェア コンポーネントとは独立したスタンドアロン ドライバー パッケージを 1 つまたは複数のソフトウェア モジュールをインストールできます。  インストールされているソフトウェアは、デバイスの価値を向上し、基本的なデバイス機能の必要はありませんが、関連付けられている関数のドライバー サービスは必要ありません。  

このページは、ソフトウェア コンポーネントの使用に関するガイドラインを提供します。

## <a name="getting-started"></a>概要

コンポーネントを作成する、[拡張子 INF ファイル](using-an-extension-inf-file.md)を指定します、 [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)で 1 つまたは複数回、 [INF DDInstall.Components](inf-ddinstall-components-section.md)セクション。  拡張子 INF ファイルで参照されているソフトウェアのコンポーネントのソフトウェア列挙子の仮想デバイスが作成されます。  1 つ以上のドライバー パッケージには、同じソフトウェア コンポーネントを参照できます。 

仮想デバイスの子ことができます依存せずに更新、他のデバイスと同じように限り、親デバイスが起動されます。  多くのさまざまなグループからの観点でのサービスと各グループの 1 つのソフトウェア コンポーネントを作成し、妥当なに機能を分離することをお勧めします。

各ソフトウェア コンポーネントに対して、INF ファイルを提供します。

ソフトウェア コンポーネント INF が指定されている場合、 [ **AddSoftware**ディレクティブ](inf-addsoftware-directive.md)コンポーネントの INF:

* 必要があります、[ユニバーサル INF ファイル](../install/using-a-universal-inf-file.md)します。
* 指定する必要があります、 **SoftwareComponent**クラスをセットアップします。

指定することができます、 [ **AddSoftware**ディレクティブ](inf-addsoftware-directive.md)1 回以上。

>[!NOTE]
>種類 2 の AddSoftware ディレクティブを使用して、コンポーネント INF を使用する必要はありません。  ディレクティブは、任意の INF で正常に使用できます。  ただし、型の 1 の AddSoftware ディレクティブは、コンポーネント INF から使用する必要があります。

さらに、任意の INF (コンポーネントかどうか) ソフトウェア コンポーネントのデバイスで一致します。

* Win32 のユーザーのサービスを使用して指定できます、 [AddService ディレクティブ](inf-addservice-directive.md)します。
* 使用したソフトウェアをインストールすることができます、 [INF AddReg ディレクティブ](inf-addreg-directive.md)と[INF CopyFiles ディレクティブ](inf-copyfiles-directive.md)します。
* 関数のドライバー サービスは必要ありません。
* ユーザーとは独立して、親デバイスからアンインストールできます。

コンポーネント INF の例を見つけることができます、[ユニバーサル ドライバーのドライバー パッケージのインストール ツールキット](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)します。

**注意**:関数へのコンポーネントのソフトウェアで列挙されるデバイスで、その親を開始する必要があります。 親デバイスで利用できるドライバーがない場合、ドライバー開発者向けは独自に作成し、必要に応じて"umpass.sys"パススルーのドライバーを利用できます。 このドライバーが Windows に含まれ、実際は何も以外のデバイスを起動します。 Umpass.sys を使用するには、開発者がで Include/Needs INF ディレクティブを使用する必要があります、 [DDInstall セクション](inf-ddinstall-section.md)の可能性のある各 [DDInstall\*] セクションで、対応する [UmPass。\*] セクションに示すよう。次に関係なくかどうか、INF ディレクティブを指定、そのセクションのか。

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

## <a name="accessing-a-device-from-a-software-component"></a>ソフトウェアのコンポーネントからデバイスへのアクセス

ソフトウェアのコンポーネントに関連付けられているデバイスのデバイス インスタンス ID を取得する、 **SoftwareArguments**値、 [INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)セクションで、`<<DeviceInstanceID>>`ランタイムコンテキスト変数を指定します。

実行可能ファイルは、その入力された引数リストからソフトウェア コンポーネントのデバイス インスタンス ID を取得できます。  

次に、ソフトウェア コンポーネントが汎用を対象とする場合[ターゲット プラットフォーム](../develop/windows-10-editions-for-universal-drivers.md)、次の手順します。

1. 呼び出す[ **CM_Locate_DevNode** ](https://msdn.microsoft.com/library/windows/hardware/ff538742)デバイスにデバイス ハンドルを取得するソフトウェア コンポーネントの ID をインスタンス化します。
2. 呼び出す[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)をそのデバイスの親を識別するハンドルを取得します。  この親が使用するソフトウェア コンポーネントを追加するデバイスでは、 [INF AddComponent ディレクティブ](inf-addcomponent-directive.md)します。
3. 次に、親のデバイス インスタンス ID を取得する呼び出し[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)からハンドル[ **CM_Get_Parent**](https://msdn.microsoft.com/library/windows/hardware/ff538610)します。

ソフトウェア コンポーネントが、デスクトップを対象とする場合[ターゲット プラットフォーム](../develop/windows-10-editions-for-universal-drivers.md)のみ、次の手順を使用します。

1. 呼び出す[ **SetupDiCreateDeviceInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550956)空のデバイス情報を作成するには設定します。
2. 呼び出す[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)ソフトウェア コンポーネントのデバイスのデバイスとインスタンス id。
3. 呼び出す[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)で`DEVPKEY_Device_Parent`親デバイス インスタンス ID を取得します。

## <a name="example"></a>例

次の例では、実行可能ファイルを使用して、グラフィックス カードのコントロール パネル をインストールするソフトウェア コンポーネントを使用する方法を示します。

### <a name="driver-package-inf-file"></a>ドライバー パッケージ INF ファイル

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

### <a name="software-component-inf-file"></a>ソフトウェア コンポーネントの INF ファイル

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

ドライバーの検証と送信のプロセスは、通常 Inf とコンポーネント Inf のと同じです。 詳細については、次を参照してください。 [Windows HLK Getting Started](https://msdn.microsoft.com/library/windows/hardware/dn915002)します。

セットアップ クラスの詳細については、次を参照してください。[ベンダー デバイス セットアップ クラスできるベンダー](https://msdn.microsoft.com/library/windows/hardware/ff553426)します。

## <a name="see-also"></a>参照

[INF AddComponent ディレクティブ](inf-addcomponent-directive.md)

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)

[INF DDInstall.Components セクション](inf-ddinstall-components-section.md)

[INF DDInstall.Software セクション](inf-ddinstall-software-section.md)
