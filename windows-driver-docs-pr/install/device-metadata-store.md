---
title: デバイス メタデータのストア
description: デバイス メタデータのストア
ms.assetid: 59af6173-28f3-44f5-874e-305bf570d683
keywords:
- デバイス メタデータ ストア WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34758c5bec60d815e183f6165bc18f2e26dd5517
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335267"
---
# <a name="device-metadata-store"></a>デバイス メタデータのストア


デバイスのメタデータ ストアは、ローカル コンピューターのデバイス メタデータ パッケージが保存されるディレクトリです。 デバイスのメタデータ ストアは、次のディレクトリからアクセスします。

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\<locale>
```

&lt;ロケール&gt;サブディレクトリは、デバイス メタデータ パッケージのロケールを表します。 このサブディレクトリの名前は、次の形式にすることができます。

```cpp
<Language>[-<Region>] 
```

たとえば、値が EN-US のでは、米国の英語の言語にローカライズされたデバイス メタデータ パッケージを含むサブディレクトリを指定します。

もしも*&lt;言語&gt;* を指定すると、デバイス メタデータを含むサブディレクトリがパッケージに言語が存在するすべての場所で指定された言語にローカライズされました。 たとえばに 'EN' の値が適用されます ' EN-US と EN BR。

デバイス メタデータ パッケージは、次の方法のいずれかで、デバイスのメタデータ ストアにコピーされます。

-   OEM または開発者は、デバイス メタデータ パッケージをコピーします。 詳細については、次を参照してください。[手動で追加するデバイス メタデータ パッケージ](manually-adding-device-metadata-packages.md)します。

-   OEM によって提供されるアプリケーションを使用して、デバイス メタデータ パッケージがコピーされます。 詳細については、次を参照してください。[アプリケーションを通じてデバイス メタデータ パッケージをインストールする](installing-device-metadata-packages-through-an-application.md)します。

**注**  はお勧めしませんそのエンドユーザー コピー デバイス メタデータ パッケージをデバイスのメタデータ ストアにします。 代わりに、エンドユーザーはいずれかを使用してデバイス メタデータ パッケージをインストールする必要があります、 [Windows メタデータとインターネット サービス (WMIS)](installing-device-metadata-packages-from-wmis.md)または OEM によって提供されるアプリケーション。

 

 

 





