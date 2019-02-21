---
title: 1 つの PDO を MFP でスキャン機能をインストールします。
description: 1 つの PDO を MFP でスキャン機能をインストールします。
ms.assetid: 002ff319-42f9-4034-9bdd-c1e771ed2ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e33176f5755e52f07f374caa4432f41c138991a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537458"
---
# <a name="installing-scanning-functionality-in-an-mfp-with-a-single-pdo"></a>1 つの PDO を MFP でスキャン機能をインストールします。





単一の物理デバイス オブジェクト (PDO) のみを持つ多機能プリンターでスキャン機能をインストールするには、特別な手順が必要です。 デバイスは、プリンター自体を識別する場合、プリンターの INF ファイルはスキャン機能をインストールするには、WIA 共同インストーラーを呼び出すことができます。

マイクロソフトでは、多機能プリンターの各論理関数を可能であれば、独自の PDO 設定ならないことをお勧めします。 デバイスの複数の関数に関連付ける 1 つの PDO は避ける必要があります。

デバイスの共同インストーラーとして WIA 共同インストーラーを登録すると、セットアップは常にプリンター クラスのインストーラーの前後に、インストールを処理する WIA 共同インストーラーを呼び出します。 WIA 共同インストーラーは、プリンターの PDO をイメージ クラス デバイス インターフェイスを作成し、デバイス インターフェイスのレジストリ キーに必要なすべての情報を格納します。 このキーの現在の場所をレジストリには。

**HKLM\\システム\\CurrentControlSet\\コントロール\\DeviceClasses\\{6bdd1fc6-810f-11d0-bec7-08002be2092f}\\&lt;*デバイス シンボリック リンク*&gt;**

このキーは、この場所の将来のオペレーティング システムのバージョンのままには保証されません。 このキーを開くには、呼び出す[ **SetupDiOpenDeviceInterfaceRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552075)します。

WIA サービスでは、すべてのイメージ クラス Pdo とデバイスのインターフェイスを列挙します。 そのため、WIA デバイスとして新しく作成したデバイスのインターフェイスが列挙されます。

INF PDO は 1 つだけ備えた多機能プリンターでスキャン機能をインストールする例を使用して Windows DDK が同梱されています。 このファイルの名前は*mfpoemprn.inf*にある、  *\\src\\印刷\\inf*ディレクトリ。

**MFP スキャン機能をインストールするには**

1.  1. 指定*sti\_ci.dll*のエントリの値として、 **CoInstallerEntry**エントリ。

    デバイスの INF 必要があります、 [ **INF DDInstall.CoInstallers セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547321)デバイスのインストールの共同インストーラーを登録できるようにします。 このセクションは次のようになります。

    ```INF
    [OEMMFP.GPD.CoInstallers]
    AddReg=WIA.CoInstallers.AddReg

    [WIA.CoInstallers.AddReg]
    HKR,,CoInstallers32,0x00010000,"sti_ci.dll, CoInstallerEntry"
    ```

2.  2.、 **WIASection**内のエントリ、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344) WIA 関連の設定すべてを含むセクションを参照します。 WIA 関連の設定を格納しているセクションは、同じ INF ファイルに表示する必要があります。

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

    含めることによって、 **WIASection**エントリ、イメージ クラスのインストーラーは、デバイスの devnode は作成されませんが、代わりに、追加のデバイスのインターフェイスを作成します。 したがって、STI-を格納する前に説明したデバイス インターフェイスのレジストリ キーを使用/WIA に関連する情報。

3.  3. ことを確認して、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)必要なすべてのファイルをコピーします。

    コピーするファイルの一覧を表示する代わりに、 **WIASection**、それらは表示されませんデバイス マネージャーが、します。

**注**   、 **Include**と**必要がある**エントリでは使用できません、 **WIASection**セクション。
カーネル モードのすべての部分は、元によるインストールが[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。

デバイスは、ホット-プラグ可能な独自のカーネル モード コンポーネントが必要な場合、は、作成して、イメージ クラスのデバイス インターフェイス (その他のクラス デバイス インターフェイスに加えて、印刷クラスのデバイスのインターフェイスなど) を有効にするにする必要があります。 カーネル モード コンポーネントへの呼び出しを使用して、デバイスの devnode では、イメージ クラス デバイス インターフェイスを有効に、 [ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)関数。 イメージ クラスのデバイスのインターフェイスが有効にすると、デバイスが接続されていることを WIA サービスに通知するプラグ アンド プレイ イベントが発生します。

 

 

 




