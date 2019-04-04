---
title: MUX 中間ドライバーのインストール
description: MUX 中間ドライバーのインストール
ms.assetid: 9d0c6d6f-c12f-4921-b08a-b23b7d96ccd9
keywords:
- MUX 中間ドライバー WDK
- NDIS MUX 中間ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c05a055a4a2363e830364e2234c2af1f6b7ba6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581805"
---
# <a name="mux-intermediate-driver-installation"></a>MUX 中間ドライバーのインストール





このトピックでは、MUX 中間ドライバーのインストールに関する問題の概要を示します。 中間ドライバーの INF ファイルの構造については、[ネットワーク MUX 中間ドライバーのインストール要件](installation-requirements-for-network-mux-intermediate-drivers.md)を参照してください。

MUX 中間ドライバーでは、2 つの INF ファイルが必要です。 プロトコルの INF ファイルでは、プロトコルの下端のインストール パラメーターを定義します。 ミニポートの INF ファイルでは、仮想ミニポートの上端のインストール パラメーターを定義します。 設定、**クラス**INF ファイルのエントリを**Net**仮想ミニポート INF ファイルで、 **NetTrans**プロトコル INF ファイル。 次のコード例は、**クラス**プロトコル INF ファイルのエントリ。

```INF
Class = NetTrans
```

*DDInstall* MUX 中間ドライバーの INF ファイルのセクションがあります、**特性**エントリ。 定義、**特性**の次のコード例に示すプロトコル INF ファイルのエントリ。

```INF
Characteristics = 0x80
```

NCF\_HAS\_通知オブジェクトこの例では、カスタム プロパティ ページを有効にする UI (0x80) が必要です

定義、**特性**ミニポート INF ファイルの次のコード例に示すように入力します。

```INF
Characteristics = 0x21
```

**特性**0x21 の値を NCF を示します\_仮想 (0x1) および NCF\_いない\_ユーザー\_リムーバブル (0x20) フラグが設定されます。 NCF\_仮想では、デバイスが仮想アダプターを指定します。 NCF\_いない\_ユーザー\_リムーバブル記憶域は省略可能であり、ユーザーが中間のドライバーを削除できないことを指定します。 (する必要がありますいないこれを行う場合は、ユーザーがデバイスを手動でインストールする必要があります)、ユーザーから仮想ミニポートを非表示にする場合は、NCF を定義できます\_(0x8) を非表示フラグ。 NCF\_*Xxx* Netcfgx.h でフラグが定義されます。 詳細については、**特性**エントリおよび NCF\_*Xxx*フラグを参照してください[DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

*DDInstall* MUX 中間ドライバー用のプロトコル INF ファイルのセクションを含める必要があります、 **Addreg**ディレクティブを**Ndi**キー。 詳細については、[Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)と[DDInstall.Services セクション](ddinstall-services-section-in-a-network-inf-file.md)を参照してください。

INF ファイルに加えて MUX 中間ドライバーを使用した通知オブジェクトを指定することも必要があります。 通知オブジェクトは、仮想ミニポートのインストールを担当します。 通知オブジェクトを参照して、 **ComponentDll**で次のように、プロトコル INF エントリ。

```INF
HKR, Ndi,            ComponentDll,   , mux.dll
```

ユーザーは、構成パラメーターを定義し、インストール ファイルをコピーしも通知オブジェクトの DLL をインストール、プロトコル INF ファイルをインストールします。 ユーザーは、通知オブジェクトによって提供されるユーザー インターフェイスを通じて仮想ミニポートを追加します。 ミニポート INF ファイルを定義する必要があります、 **ExcludeFromSelect**ユーザーがプロトコル INF ファイルではなくミニポート INF ファイルをインストールするを防ぐためエントリ。

ドライバーに登録プロトコルの名前は、サービス名と一致する必要があります。

```INF
HKR, Ndi, Service, 0, MUXP
```

**UpperRange**と**LowerRange** INF ファイルのエントリが MUX 中間ドライバーのバインドを決定します。 プロトコル INF ファイルは、次のコード例に示すよう、プロトコルの edge バインドを定義する必要があります。

```INF
HKR, Ndi\Interfaces, UpperRange,    0,          "noupper"
HKR, Ndi\Interfaces, LowerRange,    0,          "ndis5"
```

ミニポート INF ファイルは、次のコード例のように、上端バインドを定義する必要があります。

```INF
HKR, Ndi\Interfaces,    UpperRange, 0,  "ndis5"
HKR, Ndi\Interfaces,    LowerRange, 0,  "nolower"
```

"Ndis5"プロトコルのバインドで上記のコード例では、ドライバーで必要なを置き換える必要があります。 中間のドライバーのバインディングの詳細については、 **UpperRange**/**LowerRange**エントリを参照してください[中間ドライバー UpperRange と LowerRange INF ファイルエントリ](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)します。

 

 





