---
title: NetClient コンポーネントの名前とプロバイダー パスの指定
description: NetClient コンポーネントの名前とプロバイダー パスの指定
ms.assetid: 4c9c2162-8e7e-44dc-a97c-81074071664b
keywords:
- 追加レジストリ セクション WDK ネットワーク、ネットワーク クライアント コンポーネントの名前とパス
- ネットワーク クライアント コンポーネントの名前とパスの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78a1100794641c826466c159a58c44d15014b8a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388126"
---
# <a name="specifying-the-name-and-provider-path-for-a-netclient-component"></a>NetClient コンポーネントの名前とプロバイダー パスの指定





ネットワーク クライアント コンポーネントをインストールする INF ファイルを追加する必要があります、 **NetworkProvider**キーを*サービス*コンポーネントのキー。 INF ファイルを追加、 **NetworkProvider**を通じてキー、*追加レジストリ セクション*によって参照される、 **AddReg**ディレクティブで、*サービスのインストール*コンポーネントのセクション。

**NetworkProvider**キーが 2 つの値:**名前**、ネットワーク プロバイダーの名前を指定して、 **ProviderPath**ネットワークへの完全パスを指定します。プロバイダー DLL です。

例を次に、*追加レジストリ セクション*を追加する、 **NetworkProvider**コンポーネントのインスタンス キーにキー。

```INF
[NWCWorkstation.AddReg]
HKR, NetworkProvider, Name, 0, "NetWare or Compatible Network"
HKR, NetworkProvider, ProviderPath, 0x20000, "%11%\nwprovau.dll"
```

**注**  をインストールする INF ファイル、 **NetClient**コンポーネントが更新する必要はありません、 **ProviderOrder**コンポーネントの下にある値.**コントロール\\ネットワーク\\プロバイダー\\順序**キー。 これは、ネットワーク クラスのインストーラーによって自動的に行われます。

 

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

 

 





