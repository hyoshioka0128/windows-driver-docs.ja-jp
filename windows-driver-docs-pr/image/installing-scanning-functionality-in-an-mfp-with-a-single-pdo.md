---
title: 1つの PDO を使用して、MFP にスキャン機能をインストールする
description: 1つの PDO を使用して、MFP にスキャン機能をインストールする
ms.assetid: 002ff319-42f9-4034-9bdd-c1e771ed2ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a359e0cdb4beb68519268eca1b17f7074af475eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840814"
---
# <a name="installing-scanning-functionality-in-an-mfp-with-a-single-pdo"></a>1つの PDO を使用して、MFP にスキャン機能をインストールする





1つの物理デバイスオブジェクト (PDO) のみを備えた多機能プリンターにスキャン機能をインストールするには、特別な手順が必要です。 デバイスがプリンターとして識別する場合、プリンターの INF ファイルは、スキャン機能をインストールするために、WIA 共同インストーラーを呼び出すことができます。

Microsoft では、可能な限り、多機能プリンターの各論理機能に独自の PDO を用意することをお勧めします。 1つの PDO にデバイスの複数の機能を関連付けることは避けてください。

WIA 共同インストーラーをデバイスの共同インストーラーとして登録すると、セットアップでは常に、プリンタークラスのインストーラーの前後のインストールを処理するために、WIA 共同インストーラーが呼び出されます。 WIA 共同インストーラーは、プリンターの PDO にイメージクラスのデバイスインターフェイスを作成し、必要なすべての情報をデバイスインターフェイスのレジストリキーに格納します。 このキーのレジストリ内の現在の場所は次のとおりです。

**HKLM\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses\\{}\\&lt;*デバイスのシンボリックリンク*&gt;**

このキーは、今後のオペレーティングシステムのバージョンでは、この場所に保持されることは保証されていません。 このキーを開くには、 [**SetupDiOpenDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)を呼び出します。

WIA サービスは、すべてのイメージクラスの PDOs およびデバイスインターフェイスを列挙します。 そのため、新しく作成されたデバイスインターフェイスは、WIA デバイスとして列挙されます。

Windows DDK には、1つの PDO のみを備えた多機能プリンターにスキャン機能をインストールするサンプル INF が付属しています。 このファイルの名前は、 *\\src\\print\\inf*ディレクトリに*配置され*ており、このファイルの名前はです。

**MFP にスキャン機能をインストールするには**

1.  1. **Coインストーラエントリ**エントリのエントリ値として、構成*項目の\_* を指定します。

    デバイスのインストールのために共同インストーラーを登録するには、デバイスの INF に[**Inf Ddinstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)が必要です。 このセクションは、次のようになります。

    ```INF
    [OEMMFP.GPD.CoInstallers]
    AddReg=WIA.CoInstallers.AddReg

    [WIA.CoInstallers.AddReg]
    HKR,,CoInstallers32,0x00010000,"sti_ci.dll, CoInstallerEntry"
    ```

2.  2. [ [**INF DDInstall] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に、WIA 関連のすべての設定を含むセクションを参照する**WIASection**エントリを含めます。 WIA 関連の設定を含むセクションは、同じ INF ファイルに記述する必要があります。

    ```INF
    [OEMMFP.GPD]
    CopyFiles=@OEMMFP.DLL,@OEMPRT1.DLL,@OEMUI.DLL,OEMMFP.GPD.WIA.CopyFiles
    WIASection=OEMMFP.GPD.WIA

    [OEMMFP.GPD.WIA]
    Description=%OEM_MFP_SCANNER%
    SubClass=StillImage
    DeviceType=1
    Capabilities=0x00000011
    AddReg=OEMMFP.GPD.WIA.AddReg
    DeviceData=OEMMFP.GPD.WIA.DeviceData
    ICMProfiles="sRGB Color Space Profile.icm"
    USDClass="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"
    ```

    イメージクラスインストーラーでは、 **WIASection**エントリをインクルードすることによって、デバイスの devnode は作成されません。代わりに、追加のデバイスインターフェイスが作成されます。 それに伴い、前述のデバイスインターフェイスレジストリキーを使用して、関連情報を格納します。

3.  3. [ [**INF DDInstall] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に必要なすべてのファイルがコピーされていることを確認します。

    または、 **WIASection**にコピーするファイルを一覧表示することもできますが、デバイスマネージャーには表示されません。

**WIASection**セクションでは、 **Include**および**必要**なエントリを使用できませ**ん  。**
すべてのカーネルモード部分は、元の[**INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)によってインストールされている必要があります。

デバイスがホットプラグ可能で、独自のカーネルモードコンポーネントが必要な場合は、イメージクラスのデバイスインターフェイスを作成して有効にする必要があります (出力クラスのデバイスインターフェイスなど、他のクラスのデバイスインターフェイスに加えて)。 カーネルモードコンポーネントを使用すると、 [**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)関数を呼び出すことによって、デバイスの devnode 上でイメージクラスのデバイスインターフェイスを有効にすることができます。 イメージクラスのデバイスインターフェイスを有効にすると、プラグアンドプレイイベントが発生し、デバイスが接続されていることを WIA サービスに通知します。

 

 

 




