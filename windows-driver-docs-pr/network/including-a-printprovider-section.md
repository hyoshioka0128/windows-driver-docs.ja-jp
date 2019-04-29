---
title: PrintProvider セクションを含める
description: PrintProvider セクションを含める
ms.assetid: 2cbf1b56-e603-4a21-a1d7-d51634c91456
keywords:
- INF ファイルの WDK ネットワーク、した PrintProvider セクション
- ネットワーク INF ファイル、WDK した PrintProvider セクション
- した PrintProvider セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ecd949a2278e56790f3ad9b37f6531bf4362605
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327776"
---
# <a name="including-a-printprovider-section"></a>PrintProvider セクションを含める





インストールする INF ファイル、 **NetClient**印刷プロバイダーであるコンポーネントを含める必要があります、**した PrintProvider**そのコンポーネントのセクション。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

作成する、**した PrintProvider**セクションで、追加、**した PrintProvider**拡張機能を*DDInstall*の次の例に示すように、コンポーネントのセクションします。
```cpp
[DDInstall-section] ; Install section
[DDInstall-section.PrintProvider] ; PrintProvider section
```

**した PrintProvider**セクションは、次のエントリを含める必要があります。

<a href="" id="printprovidername"></a>**PrintProviderName**  
印刷のプロバイダーの名前を指定する非ローカライズ文字列。

<a href="" id="printproviderdll"></a>**PrintProviderDll**  
印刷プロバイダーの DLL のファイル名。

<a href="" id="displayname"></a>**DisplayName**  
印刷のプロバイダーの名前を指定するローカライズ可能な文字列。 **DisplayName**とは異なる、 **PrintProviderName**します。

**PrintProviderName**と**PrintProviderDll**エントリが入力として使用される情報を指定 (、PROVIDOR で\_情報\_1 構造) に、 **AddPrintProvidor**関数。 **AddPrintProvidor**関数は、印刷プロバイダーとして、印刷プロバイダー コンポーネントを追加します。 詳細については、 **AddPrintProvidor**関数を Microsoft Windows SDK を参照してください。

例を次に、**した PrintProvider**セクション。

```cpp
[DDnstall-section.PrintProvider]
PrintProviderName = "NetWare or Compatible Network"
PrintProviderDll  = "nwprovau.dll"
DisplayName       = "%NWC_Network_Display_Name%"
```

 

 





