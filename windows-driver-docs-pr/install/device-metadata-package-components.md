---
title: デバイス メタデータのパッケージ構造
description: デバイス メタデータのパッケージ構造
ms.assetid: 37614100-0a56-4a32-8e45-3161994e503a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3932c57925a4bd544bb20e6ef24f475e122dc5a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569932"
---
# <a name="device-metadata-package-structure"></a>デバイス メタデータのパッケージ構造


各デバイス メタデータ パッケージは、次のディレクトリ構造があります。

PackageInfo.xml

DeviceInformation DeviceInfo.xml *DeviceIcon*.ico

WindowsInformation WindowsInfo.xml

デバイス メタデータ パッケージを作成する DeviceStage 場合に、XML ドキュメントとアイコン ファイルは、次のディレクトリに格納されます。

-   [PackageInfo XML ドキュメント](packageinfo-xml-document.md)がディレクトリのルートにあります。 この XML ドキュメントの名前は、PackageInfo.xml である必要があります。

-   DeviceInformation サブディレクトリが含まれています、 [DeviceInfo XML ドキュメント](deviceinfo-xml-document.md)と省略可能なデバイスのアイコン ファイル。 XML ドキュメントの名前は、DeviceInfo.xml である必要があります。

    任意の名前を持つことができますのサフィックスで終わる必要がありますが、デバイス メタデータ パッケージには、デバイスのアイコン ファイルが含まれている場合 *.ico*します。 詳細については、次を参照してください。[デバイス アイコン ファイル](device-icon-file.md)します。

-   WindowsInformation サブディレクトリが含まれています、 [WindowsInfo XML ドキュメント](windowsinfo-xml-document.md)します。 XML ドキュメントの名前は、WindowsInfo.xml である必要があります。

-   DeviceStage サブディレクトリには、Device Stage エクスペリエンスを提供する Windows デバイスのステージで使用される特定のファイルが含まれています。 Device Stage は、開発およびデバイス固有のエクスペリエンスを配布するための豊富なプラットフォームです。 Device Stage をデバイス メーカーはブランドに合わせて、機能、およびそのデバイスのサービスのみいくつかの XML ファイルとグラフィックスを定義することでエクスペリエンスを作成できます。

    デバイス メーカーは、デバイスの Device Stage エクスペリエンスを使用している場合、Windows には、デバイス メタデータ パッケージである DeviceStage ディレクトリが必要です。 それ以外の場合、Windows は、パッケージ内にある場合、ディレクトリを無視します。

    **注**Device Stage が限られた数のデバイス クラスのサポートされています。




Windows デバイス エクスペリエンス、Device Stage、およびデバイス ステージの XML スキーマの詳細が記載されて、 [Microsoft デバイス エクスペリエンス開発キット](https://go.microsoft.com/fwlink/p/?linkid=192621)します。


デバイス メタデータ パッケージを作成するときにこれらのガイドラインに従ってください。

-   Utf-8 エンコーディングを使用して、各 XML ドキュメントを保存する必要があります。

-   デバイス メタデータ パッケージは、デバイスのアイコンを含める必要はありません。 ただし、強くお勧め、デバイス メタデータ パッケージを含む、[デバイス アイコン ファイル](device-icon-file.md)します。 これは、デバイスとプリンターでデバイスの写真のようなイメージを表示に使用されます。

Windows Driver Kit (WDK) の Windows 7 バージョン以降、[トースター サンプル](https://go.microsoft.com/fwlink/p/?linkid=256195)サンプル デバイス メタデータ パッケージを提供します。 このパッケージの XML ドキュメントにある、 *src\\全般\\トースター\\devicemetadatapackage* WDK のサブディレクトリ。









