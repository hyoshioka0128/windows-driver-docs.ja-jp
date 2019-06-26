---
title: デバイス メタデータ パッケージの構築
description: デバイス メタデータ パッケージの構築
ms.assetid: 8b95a88e-430c-4250-959f-43536fdc1824
keywords:
- デバイス メタデータ パッケージ WDK では、ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b31847458599f3bfc7a617f3c5400bfb49ce790
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385291"
---
# <a name="building-device-metadata-packages"></a>デバイス メタデータ パッケージの構築


このトピックでは、デバイス メタデータ パッケージを構築する方法のガイドラインを提供します。

### <a href="" id="device-metadata-package-file-names"></a> デバイス メタデータ パッケージのファイル名

デバイス メタデータ パッケージのファイルを作成する前にまずメタデータ パッケージのグローバル一意識別子 (GUID) を作成する必要があります。 これを行うには、Guidgen ツールを使用して *(Guidgen.exe*) に記載されている、 [GUID 生成](https://go.microsoft.com/fwlink/p/?linkid=145426)web サイト。

デバイス メタデータ パッケージのファイル名には、次の名前付け規則を使用する必要があります。

```cpp
<GUID>.devicemetadata-ms
```

たとえば、{20f001a99-4675-8707-248ca-187dfd9} の値を持つ GUID を作成する場合は、次のデバイス メタデータ パッケージ ファイルを作成するその GUID を使用します。

```cpp
20f001a99-4675-8707-248ca-187dfd9.devicemetadata-ms
```

**注**  オペレーティング システムのサフィックスを持つ場合にのみデバイス メタデータ パッケージは認識されます *。devicemetadata ms*します。

 

デバイス メタデータ パッケージのファイルに次の規則が適用されます。

-   各メタデータ パッケージのファイル名の GUID は一意である必要があります。 新規または変更されたメタデータ パッケージを作成するときに、変更はわずか場合でも、新しい GUID を作成する必要があります。

-   各メタデータ パッケージは、1 つだけのロケールをサポートできます。 デバイスの 1 つ以上のロケールをサポートする場合は、独自の GUID を持つ各メタデータ パッケージと、ロケールごとに別のメタデータ パッケージを作成する必要があります。 詳細については、次を参照してください。 [**ロケール XML 要素**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548647(v=vs.85))します。

    **注**  デバイスのロケールに固有のデバイス メタデータ パッケージの複数のファイルが必要な場合、言語に依存しない識別子を作成してでのすべてのファイルをグループ化できます。 この識別子は、GUID とで同じ GUID を指定できます、 [ **LanguageNeutralIdentifier** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548617(v=vs.85))同じデバイスのすべてのメタデータ パッケージ内の XML 要素。

     

-   *&lt;GUID&gt;* デバイス メタデータ パッケージのファイル名のプレフィックスなしの GUID を指定する必要があります、' {' または '}' の区切り記号。

### <a name="creating-a-device-metadata-package-file"></a>デバイス メタデータ パッケージ ファイルを作成します。

[デバイス メタデータ パッケージのコンポーネント](device-metadata-package-components.md)、Cabarc を使用して圧縮されたファイルに格納されます (*Cabarc.exe*) ツール。 このツールの詳細についてを参照してください、 [Cabarc 概要](https://go.microsoft.com/fwlink/p/?linkid=145395)web サイト。

次のコード例では、Cabarc ツールを使用してデバイス メタデータ パッケージ ファイルを作成する方法を示します。 この例では、メタデータ パッケージのコンポーネントがという名前のローカル ディレクトリにある*MyMetadataPackage*します。 次の一覧は、サブディレクトリを示していて、ファイル内で、 *MyMetadataPackage*ディレクトリ。

```cpp
.\MyMetadataPackages
.\MyMetadataPackage\PackageInfo.xml
.\MyMetadataPackage\DeviceInformation\DeviceInfo.xml
.\MyMetadataPackage\DeviceInformation\MyIcon.ico
.\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

最初に、デバイス メタデータ パッケージの {0} f4ea2b40-77ff-443d-8212-be7e74a344ae} の値の GUID が作成されます。 次の図は、Guidgen ツールを使用して GUID を作成する方法を示します。

![guid のダイアログ ボックスの作成、guidgen のスクリーン ショット](images/dmrc.png)

次のコマンドは Cabarc ツールを使用して、という名前のローカル ディレクトリで新しいデバイス メタデータ パッケージ ファイルを作成する、 *MyDeviceMetadataPackage*:

```cpp
Cabarc.exe -r -p -P .\MyMetadataPackage\ 
    N .\MyDeviceMetadataPackage\f4ea2b40-77ff-443d-8212-be7e74a344ae.devicemetadata-ms 
    .\MyMetadataPackage\PackageInfo.xml 
    .\MyMetadataPackage\DeviceInformation\DeviceInfo.xml 
    .\MyMetadataPackage\DeviceInformation\MyIcon.ico 
    .\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

**注**  各メタデータ パッケージは、1 つだけのロケールをサポートできます。 デバイスの 1 つ以上のロケールをサポートする場合は、独自の GUID を持つ各メタデータ パッケージと、ロケールごとに別のメタデータ パッケージを作成する必要があります。

 

 

 





