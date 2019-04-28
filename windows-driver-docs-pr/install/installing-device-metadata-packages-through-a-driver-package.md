---
title: ドライバー パッケージからのデバイス メタデータ パッケージのインストール
description: ドライバー パッケージからのデバイス メタデータ パッケージのインストール
ms.assetid: fd140583-d4f9-4817-8edc-5bc3c6a2a1d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98af154c1b33bbc1f14dcad87642c9f6b6ba30b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369480"
---
# <a name="installing-device-metadata-packages-through-a-driver-package"></a>ドライバー パッケージからのデバイス メタデータ パッケージのインストール


A[ドライバー パッケージ](driver-packages.md)をコピーしてデバイス メタデータ パッケージをインストールすることができます、[デバイス メタデータ ストア](device-metadata-store.md)します。 これを使用して実現[ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)内、 [ **DestinationDirs** ](inf-destinationdirs-section.md)と[ **DDInstall** ](inf-ddinstall-section.md)のセクションでは、 [INF ファイル](inf-files.md)ドライバー パッケージ。

**注**WMIS サーバーからドライバー パッケージを通じての代わりに、デバイス メタデータ パッケージをインストールすることを強くお勧めします。 詳細については、次を参照してください。 [WMIS からデバイス メタデータ パッケージをインストールする](installing-device-metadata-packages-from-wmis.md)します。



デバイス メタデータ パッケージをインストールする、[ドライバー パッケージ](driver-packages.md)、これらのガイドラインに従う必要があります。

-   デバイス メタデータ パッケージをコピーする必要があります、[デバイス メタデータ ストア](device-metadata-store.md)INF ディレクティブを使用しています。 によって、メタデータ パッケージをコピーしない必要があります、[共同インストーラー](writing-a-co-installer.md)します。

-   Windows 7 より前のバージョンの Windows デバイスをインストールするドライバー パッケージを使用する場合、個別を使用する必要があります[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)を格納している、メタデータに関連する INF ディレクティブ。 このセクションの名前を指定する必要があります、 [ **INF*モデル*セクション**](inf-models-section.md)を使用して、 *TargetOSversion*装飾、を指定します。*OSMajorVersion*と*OSMinorVersion* Windows 7 または Windows の以降のバージョンの値。

    **注**個別 INF を使用しない場合*DDInstall* Windows 7 または Windows でのデジタル署名されたインストールの以降のバージョンの装飾したセクション[ドライバー パッケージ](driver-packages.md)なりますWindows 7 より前のバージョンの Windows にインストールされているときに署名のアラート。




詳細については、次を参照してください。[プラットフォーム拡張機能バージョンのオペレーティング システムと組み合わせて](combining-platform-extensions-with-operating-system-versions.md)します。


-   ドライバー パッケージ内のすべてのメタデータ パッケージを適切なロケール固有フォルダーにコピーする必要があります、[デバイス メタデータ ストア](device-metadata-store.md)します。 これは、ロケールに動的な変更をサポートするために必要です。

-   ありますフラグ (0x00000800) が必要です、 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)デバイス メタデータ パッケージを指定します。 このフラグは、デバイス メタデータ パッケージのバイナリの整合性が保持され、ドライバー パッケージがインストールされている場合は、デバイス メタデータ パッケージの圧縮解除を回避できますが保証されます。

-   必要があります最初にデジタル署名デバイス メタデータ パッケージ、ドライバー パッケージにデジタル署名する前にします。 デジタル署名の詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

-   メタデータ パッケージのインストールのインストール中に、エラーをすべてでは、ドライバーのインストールが失敗すると、します。

次の例では、ロケール固有のディレクトリ パスに、デバイスのメタデータ ストア内の INF ファイルを使用してデバイス メタデータ パッケージをコピーする方法を示しています、 [ **DestinationDirs セクション**](inf-destinationdirs-section.md)と[**DDInstall** ](inf-ddinstall-section.md) INF セクション。

```cpp
[SourceDisksNames]
1 = %Media_Description%,,,\MetadataPackage ;

[SourceDisksFiles.NTx86]
GUID1.devicemetadata-ms= 1,, ;A metadata package file for EN-US
GUID2.devicemetadata-ms= 1,, ;A metadata package file for AR-SA
GUID3.devicemetadata-ms= 1,, ;A metadata package file for JA-JP

[DestinationDirs]
COPYMETADATA_EN-US = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\EN-US ;
COPYMETADATA_AR-SA = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\AR-SA ;
COPYMETADATA_JA-JP = 24, \ProgramData\Microsoft\Windows\DeviceMetadataStore\JA-JP ;
. . .

[DeviceInstall.ntx86]
CopyFiles=COPYMETADATA_EN-US
CopyFiles=COPYMETADATA_AR-SA
CopyFiles=COPYMETADATA_JA-JP

[COPYMETADATA_EN-US]
GUID1.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
[COPYMETADATA_AR-SA]
GUID2.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
[COPYMETADATA_JA-JP]
GUID3.devicemetadata-ms,,,0x00000800 ;COPYFLG_NODECOMP
```









