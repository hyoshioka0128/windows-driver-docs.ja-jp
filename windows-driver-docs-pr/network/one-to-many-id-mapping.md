---
title: ID の一対多のマッピング
description: ID の一対多のマッピング
ms.assetid: 395d3f20-7410-496b-9ec3-1052cd731ae3
keywords:
- マッピングのネットワーク コンポーネント Id
- ID マッピングの WDK netmap.inf ファイル
- 一対多 ID マッピングの WDK ネットワーク
- アップグレード前の Id の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00afe01ebf2b07208652a2eda65b56505901805
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537190"
---
# <a name="one-to-many-id-mapping"></a>ID の一対多のマッピング





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

一対多の ID マッピングは、1 つ以上のネットワーク アダプタを表す 1 つのアップグレード前 ID をマップします。 1 つのアップグレード前の ID に関連付けられているアダプターを区別する唯一の方法では、ネットワーク アダプターのインスタンスのパラメーターの値を格納するレジストリ キーの下の値を検査します。

内のエントリを**OemAdapters**または**OemAsyncAdapters**一対多の ID マッピングを指定するセクションには、次の形式。

*preupgrade-ID* = *mapping-method-number*, *section-name*

この場合

*マッピング-メソッド-番号*0 にする必要があります

*セクション名*マッピング情報を含む netmap.inf ファイルのファイルでセクションを指定します

指定した netmap.inf ファイル ファイル セクション*セクション名*次のエントリが含まれています。

**ValueName = "**<em>Name</em>**"**

ネットワーク アダプターのインスタンスのパラメーターの値を格納するレジストリ キー NetSetup を読み取る値を指定します。 *名前*特定のネットワーク アダプターを識別します。

**ValueType =** *Type*

レジストリ値の型を指定します*ValueName*します。 *型*は特定のレジストリの型に対応する整数です。

*ValueName*= *postupgrade-ID*

*ValueName* NetSetup を読み取り、ネットワーク アダプターのインスタンスのパラメーターの値を格納するレジストリ キーの下の値です。 *postupgrade ID*が Windows 2000 またはアダプターの以降のデバイス ID。 1 つ*ValueName*アップグレードされる各アダプターの種類には、エントリを指定する必要があります。 場合*ValueName*キーワードに設定されている**ValueNotPresent** NetSetup アダプター インスタンスのパラメーターの値が見つからない、NetSetup 使用して、 *postuprgrade ID*関連付けられている**ValueNotPresent**アダプター。

次の例では、一対多のデバイス ID のマッピングを示します。

```cpp
[OemAdapters]
DATAFIREU=0, DATAFIREU

[DATAFIREU]
ValueName  = "BoardType"
ValueType  = 1
DataFireIsaU = "DATAFIRE - ISA1U"
DataFireIsa1ST= "DATAFIRE - ISA1ST"
DataFireIsa4ST= "DATAFIRE - ISA4ST"
DataFireIsaGeneric = "ValueNotPresent"
```

**OemAdapters** DATAFIREU としてネットワーク アダプターのアップグレード前のデバイス ID を識別することを指定している 1 つのエントリが上記の例のセクションに含まれています、 **DATAFIREU**のセクションで、netmap.inf ファイルのファイルには、このアダプターのマッピング情報が含まれています。

DATAFIREU セクションには、次の情報が含まれています。

-   **ValueName**エントリを探して NetSetup を指示する、 **BoardType**値、**パラメーター**ネットワーク アダプターのインスタンスのキー。

-   **ValueType**エントリで、1 に設定されていることを指定、 **BoardType**値は DWORD です。

-   残りの各値は、アップグレード前のデバイスを使用している ID と、対応する Windows 2000 またはそれ以降の ID を指定します たとえば、DataFireIsaU ボードの種類の ID は、DATAFIRE - ISA1U が。 **ValueNotPresent**アップグレード前の ID ではなくキーワードを指定することができます

NetSetup は一対多の ID を実行します。 次のようにマッピングします。

1.  NetSetup では、ネットワーク アダプターのインスタンスのパラメーターの値を格納するレジストリ キーの下で指定された ValueName を読み取ります。

2.  NetSetup が netmap.inf ファイルのファイルの指定されたセクションに表示されている値名のいずれかの値名を照合しようとするとします。 レジストリ キーの下に ValueName が表示されない場合 NetSetup netmap.inf ファイルのファイルの指定されたセクションに ValueNotPresent キーワードを検索しようとします。

3.  NetSetup には、一致が見つかると、インストール id。 同じ名前として、マップされた Windows 2000 またはそれ以降の INF ファイルを使用して、ネットワーク アダプター

レジストリ キーまたはアダプターのインスタンスの値が異なる種類のアダプターに同一の場合、これらのレジストリ キーまたは値は、初めて変更することがなくアップグレード前の 1 つのデバイス ID を 1 つ以上の Windows 2000 またはそれ以降のデバイス ID にマップすることはできません。

このような状況を処理の最も効果的な方法は次のとおりです。

1.  ネットワーク移行 DLL の[ **PreUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562439)関数は、レジストリ、ネットワーク アダプターのインスタンスごとに一意の値に含まれるように、レジストリを変更します。 これらの一意の値は、アダプターの種類を示す必要があります。

2.  **PreUpgradeInitialize**関数の設定、NUA\_要求\_中止\_NetSetup winnt32.exe を再起動し、中止するよう求めるメッセージを表示すると、アップグレードのフラグ、アップグレードします。

3.  ユーザーは、アップグレードを中止し、winnt32.exe を再起動します。 DLL のネットワークの移行、アップグレード前の 1 つのデバイス ID を 1 つ以上の Windows 2000 またはそれ以降のデバイス ID をマップするのに一意の値を使用できますようになりました

 

 





