---
title: オフラインの Windows イメージへのデバイス メタデータ パッケージのインストール
description: オフラインの Windows イメージへのデバイス メタデータ パッケージのインストール
ms.assetid: 53480324-951f-4c51-9b5b-051ce1a3b709
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8fa07b9c066b08e52724f052feec8087c3faf19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366294"
---
# <a name="installing-device-metadata-packages-to-an-offline-windows-image"></a>オフラインの Windows イメージへのデバイス メタデータ パッケージのインストール


コンピューターの Oem は、ローカル デバイスのメタデータ ストアにパッケージをコピーすることによって、Windows のオフライン イメージにデバイス メタデータ パッケージを追加できます。 このストアは、次の場所には。

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

最初に作成する必要があります、 *&lt;ロケール&gt;* デバイス メタデータ パッケージの対象のロケールに基づいてサブディレクトリ。 適切なメタデータ パッケージをコピーする必要がありますし、 *&lt;ロケール&gt;* サブディレクトリ。

たとえばの英国英語にローカライズされているデバイス メタデータ パッケージは、次の場所にコピーする必要があります。

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-GB
```

日本語の言語にローカライズされているデバイス メタデータ パッケージは、次の場所にコピーする必要があります。

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\JA
```

詳細については、次を参照してください。[デバイス メタデータ ストア](device-metadata-store.md)します。

 

 





