---
title: NetworkProvider セクションを含める
description: NetworkProvider セクションを含める
ms.assetid: 8972f926-c4f5-4a2f-8f2d-f9353fdbd83f
keywords:
- INF ファイルの WDK ネットワーク、NetworkProvider セクション
- ネットワーク INF ファイル、WDK NetworkProvider セクション
- NetworkProvider セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13c6bbbc5927cf4577f5c854d9c3089950126dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327813"
---
# <a name="including-a-networkprovider-section"></a>NetworkProvider セクションを含める





A **NetworkProvider**セクションのいずれか、代替デバイス名を指定する、 **NetClient**コンポーネントまたは、NetWare で使用するための短い名前 **「net view**コマンド、またはその両方です。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

作成する、 **NetworkProvider**セクションで、追加、 **NetworkProvider**拡張機能を*DDInstall*の次の例に示すように、コンポーネントのセクションします。
```INF
[DDInstall] ; Install section
[DDInstall.NetworkProvider] ; NetworkProvider section
```

### <a name="specifying-a-device-name"></a>デバイス名を指定します。

ネットワーク クラスのインストーラーは、コピーして、ネットワーク プロバイダー、デバイス名を作成する通常の**Ndi\\サービス**NetworkProvider キー コンポーネントのコンポーネントの値**サービス**キー。 詳細については、次を参照してください。 [Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)します。 コンポーネントの別のデバイス名を指定する、 **DeviceName**内のエントリ、 **NetworkProvider**の次の例に示すように、コンポーネントのセクションします。

```INF
[DDInstall-section.NetworkProvider]
DeviceName = "nwrdr"
```

**DeviceName**省略可能であり、場合にのみ指定する必要があります、 **Ndi\\サービス**値のコンポーネントが、ネットワーク プロバイダーのデバイス名として適切ではありません。

### <a name="specifying-a-short-name"></a>短い名前を指定します。

NetWare を使用するためのネットワーク プロバイダーの短い名前を指定する **「net view**コマンド、 **ShortName**内のエントリ、 **NetworkProvider** 、コンポーネントのセクション次の例のように。

```INF
[DDInstall-section.NetworkProvider]
ShortName = "nw"
```

使用される短い名前の例を次に、 **「net view**コマンド。

```INF
net view /n:nw
```

**ShortName**記憶して、ネットワーク プロバイダーの完全な名前を入力する方が簡単です。

**ShortName**は省略可能なだけ指定した場合は必要とします。

 

 





