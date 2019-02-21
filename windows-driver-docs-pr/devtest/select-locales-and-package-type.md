---
title: ロケールを選択し、パッケージのデバイス メタデータの作成ウィザードの種類
description: ロケールを選択し、パッケージのデバイス メタデータの作成ウィザードの種類
ms.assetid: 02227FAB-A37F-4B20-AD52-E071C19E8743
keywords:
- ロケールを選択し、パッケージのデバイス メタデータの作成ウィザードの種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5693c025865ea9f4620b1ecf7861dd9e2584e7d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529852"
---
# <a name="select-locales-and-package-type-in-the-device-metadata-authoring-wizard"></a>ロケールを選択し、パッケージのデバイス メタデータの作成ウィザードの種類


開始するには、適切なロケールまたはパッケージの種類 (Windows 7 または Windows 8) と同様に、メタデータ パッケージのロケールを選択します。

### <a name="span-idtosetlocaleandpackagetypespanspan-idtosetlocaleandpackagetypespanspan-idtosetlocaleandpackagetypespanto-set-locale-and-package-type"></a><span id="To_set_locale_and_package_type"></span><span id="to_set_locale_and_package_type"></span><span id="TO_SET_LOCALE_AND_PACKAGE_TYPE"></span>ロケールとパッケージの種類を設定するには

1.  をクリックして、**パッケージ定義**タブ。
2.  **利用可能なロケール**、メタデータ パッケージに関連付けるものを選択します。
    **注:**  
    この手順では、すべてのメタデータ パッケージの必要があります。

    Windows 7 のパッケージで複数の単一ロケールのデバイス メタデータ パッケージが作成されます。 Windows 8 では、複数のロケールを含む単一のメタデータ パッケージを作成します。



3.  **既定のロケール**次のいずれかの操作します。
    -   パッケージのロケールのパッケージを使用できないときに、特定の言語で表示される場合は、目的の言語を選択します。
        **注**メタデータ パッケージを 1 つは、既定のローカル パッケージとしてのみ指定できます。




-   ロケール固有のパッケージが利用でない場合は、特定の言語で表示するパッケージをしたくない場合**既定値はありません**します。


4.  画面の下部には、次のオプションのいずれかを選択します。
    -   選択**Windows 8 パッケージ (パッケージごとの複数のロケール)** 次の条件が当てはまる場合は。
        -   既定のデバイス情報を使用して、Windows 7 で**デバイスとプリンター**で**コントロール パネルの **いずれかで (たとえば、英語リソースのすべての表示言語) 言語を表示します。
        -   デバイス メタデータ パッケージの数を削減します。
    -   選択**Windows 7 スタイルのデバイス メタデータ パッケージ (パッケージごとに 1 つのロケール)** 次の条件が当てはまる場合は。
        -   特定の言語のメタデータのパッケージでは、別の言語の情報を含めることはできません。
        -   ロケールごとにデバイス情報を区別するため**デバイスとプリンター**で**コントロール パネルの **します。









