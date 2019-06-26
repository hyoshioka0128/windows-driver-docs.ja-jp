---
title: ネイティブ 802.11 IHV 拡張機能のインストール
description: ネイティブ 802.11 IHV 拡張機能のインストール
ms.assetid: 73e45572-6f48-43da-9456-4de5e1f1901f
keywords:
- IHV 拡張機能をインストールする WDK ネイティブの 802.11
- ネイティブの 802.11 IHV 拡張機能のインストール
- ネイティブ 802.11 IHV 拡張 WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0714e63eabed796726839a84c60c32449a617ebf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385847"
---
# <a name="installing-native-80211-ihv-extensions"></a>ネイティブ 802.11 IHV 拡張機能のインストール




 

インストールする、 [802.11 IHV 拡張機能のネイティブの DLL](native-802-11-ihv-extensions-dll4.md)と[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)、独立系ハードウェア ベンダー (IHV) が、INF の DDInstall」セクションに次の変更を加える必要がありますIHV のワイヤレス LAN (WLAN) アダプターのインストールに使用されるファイルです。

-   関連付けられている、CopyFiles ディレクティブを追加する*ファイルのセクション一覧*、INF ファイルにします。 IHV によって開発された各 DLL の名前は内である必要があります、*ファイルのセクション一覧*します。

    たとえば、IhvExt.dll と IhvUIExt.dll IHV のインストールは、INF ファイルになります次 CopyFiles ディレクティブと*ファイルのセクション一覧*:

    ```
    CopyFiles = Sample-File-List-Section

    [Sample-File-List-Section]
    IhvExt.dll,,,2
    IhvUIExt.dll,,,2
    ```

    CopyFiles ディレクティブの詳細については、次を参照してください。 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)します。

-   DestinationDirs セクションがのコピー先を宣言することを確認、*ファイルのセクション一覧*CopyFiles ディレクティブで使用します。

    前の例では、DestinationDirs セクションは、次の値になります。

    ```
    [DestinationDirs]
    DefaultDestDir = 11
    Sample-File-List-Section = 11
    ```

    DestinationDirs セクションの詳細については、次を参照してください。 [ **INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)します。

-   確認します AddReg ディレクティブを関連付けられている*追加レジストリ セクション*、WLAN アダプターごとに INF ファイルに追加されます。 AddReg ディレクティブの詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。

    内で、*追加レジストリ セクション*、次のキーを宣言する必要があります。

    <a href="" id="hkr--ndi-ihvextensions--extensibilitydll--0----------destination-file-name"></a>HKR、Ndi\\IHVExtensions、ExtensibilityDLL、0、*変換先ファイル名*  
    このキーは、IHV 拡張 DLL の名前を識別します。 など、IhvExt.dll WLAN アダプターの管理に関連付けるに、次のキーを宣言するとします。

    ```
    HKR,Ndi\IHVExtensions, ExtensibilityDLL, 0, %SystemRoot%\system32\IhvExt.dll
    ```

    <a href="" id="hkr--ndi-ihvextensions--uiextensibilityclsid--0----------clsid"></a>HKR、Ndi\\IHVExtensions、UIExtensibilityCLSID、0、 *CLSID*  
    このキーは、IHV UI 拡張機能の DLL のターゲット システムに登録された COM クラス識別子 (CLSID) を識別します。 *CLSID*値を引用符で囲む必要があります。 このキーは、を介してインストール IHV 拡張 DLL を IHV UI 拡張機能の DLL を関連付けます、 **ExtensibilityDLL**キー。

    **注**  、 **UIExtensibilityCLSID** IHV IHV UI 拡張 DLL をインストールする場合にのみ、キーが必要です。

     

    <a href="" id="hkr--ndi-ihvextensions--adapteroui--0x00010001----------oui"></a>HKR、Ndi\\IHVExtensions、AdapterOUI、0x00010001 *OUI*  
    このキーは、IEEE に割り当てられた組織的一意識別子 (OUI)、IHV を識別するを識別します。 OUI 値は、24 ビットの 16 進数値として宣言する必要があります。

    WLAN アダプターの OUI がの値と一致していることを確認する AdapterOUI キーが使用される、 **OUI**の属性、 **IHV** XML 要素。 詳細については、 **IHV**要素と、ネイティブの 802.11 XML スキーマが、Microsoft Windows SDK のマニュアルを参照してください。

INF ファイルとそのセクションの詳細については、次を参照してください。 [INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)します。

 

 





