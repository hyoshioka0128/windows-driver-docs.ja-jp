---
title: 通知オブジェクトのレジストリ値の追加
description: 通知オブジェクトのレジストリ値の追加
ms.assetid: 8872a9b9-b7c5-4c10-b5d4-4fe880fc436f
keywords:
- ネットワーク、インターネット接続の追加レジストリ セクション WDK 通知オブジェクトのレジストリ値
- オブジェクトの WDK ネットワーク、レジストリ値への通知します。
- ネットワーク オブジェクト、WDK のレジストリ値を通知します。
- レジストリ WDK オブジェクトに通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d859c24aae57834b214d26889f533d35ec86c05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384725"
---
# <a name="adding-registry-values-for-a-notify-object"></a>通知オブジェクトのレジストリ値の追加





A **NetTrans**、 **NetClient**、または**NetService**コンポーネントは、次の操作の 1 つ以上を実行する通知オブジェクトを持つことができます。

-   コンポーネントのユーザー インターフェイスを表示します。

-   イベントのバインド、コンポーネントがバインド プロセスをある程度の制御を練習するためのコンポーネントに通知します

-   条件付きでインストールまたはソフトウェア コンポーネントを削除します

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

詳細については、オブジェクトに通知を参照してください[ネットワーク コンポーネントの通知オブジェクト](notify-objects-for-network-components.md)します。

**注**  **Net**コンポーネント (アダプター) がないオブジェクトに通知のサポート。 したがって、これらのコンポーネントが共同インストーラーを使用する必要があります。

 

共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-co-installer)です。

コンポーネントのかどうか、通知オブジェクトが、そのコンポーネントの INF ファイルを追加する必要があります (を通じて、*追加レジストリ セクション*) コンポーネントのための値を**Ndi**キー。

<a href="" id="clsid"></a>**clsID**  
21\_通知オブジェクトの GUID (グローバル一意識別子) を指定します。 SZ 値。 Uuidgen.exe ユーティリティを実行して、この GUID を取得します。 このユーティリティの詳細については、Microsoft Windows SDK を参照してください。

<a href="" id="componentdll"></a>**ComponentDll**  
21\_通知オブジェクトの DLL へのパスを指定します。 SZ 値。 **ComponentDll** DLL は、Windows でない場合は、DLL への完全パスを指定する必要があります\\System32 ディレクトリ。

例を次に、*追加レジストリ セクション*を追加する**ClsID**と**ComponentDll**値を**Ndi**キー。

```INF
[MS_Protocol.ndi.reg]
HKR, Ndi, ClsID, 0, "GUID"
HKR, Ndi, ComponentDll, 0, "notifyobject.dll"
```

*DDInstall*セクションは、通知オブジェクトを持つコンポーネントも含める必要があります、 **CopyFiles**を参照するディレクティブ、*ファイルのセクション一覧*通知をコピーします。指定されたインストール先ディレクトリに DLL のオブジェクト、 **DestinationDirs**セクション。 詳細については、 **CopyFiles**ディレクティブと**DestinationDirs**のセクションを参照してください[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

 

 





