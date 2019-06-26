---
title: 別のネットワーク コンポーネントのインストールの要求
description: 別のネットワーク コンポーネントのインストールの要求
ms.assetid: 30e6db7f-46f4-414f-a485-051b007f0eb6
keywords:
- 追加レジストリ セクション WDK のネットワー キング、コンポーネントの依存関係
- コンポーネント Id の WDK ネットワーク
- コンポーネントの依存関係の WDK ネットワーク
- 依存関係の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88291647a1a4252651fcd1045588e05a17a7cb12
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378657"
---
# <a name="requiring-the-installation-of-another-network-component"></a>別のネットワーク コンポーネントのインストールの要求





ネットワーク コンポーネントは、1 つまたは複数のネットワーク コンポーネントのインストールを正常に機能するために必要があります。 ネットワーク INF ファイルでこのような各依存関係を指定します、 **RequiredAll**値。 **RequiredAll**値が追加されます (を通じて、*追加レジストリ セクション*) に、 **Ndi**が別のネットワーク インストールを必要とするネットワーク コンポーネントのキーコンポーネント。

次の例は、 **RequiredAll**内のエントリを*追加レジストリ セクション*:

```INF
[ndi.reg]
HKR, Ndi, RequiredAll, 0, "component id"
```

*コンポーネント ID*は、 *hw id*の必要なネットワーク コンポーネント。 詳細については、次を参照してください。 [ **INF モデル セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)します。 ネットワーク コンポーネントには、その他の 1 つ以上のネットワーク コンポーネントのインストールが必要とする場合は、1 つを使用して、 **RequiredAll**エントリ ネットワーク コンポーネントのごとに次の例に示すようにインストールする必要があります。

```INF
HKR, Ndi, RequiredAll, 0, "component1 id, component2 id"
```

**注**  、 **RequiredAll**値は、ユーザーがインストールできない非表示のネットワーク コンポーネントのインストールにのみ使用する必要があります。 このようなコンポーネントは、ユーザー インターフェイスをサポートしていません。 いずれかのネットワーク コンポーネントによって指定された**RequiredAll**経由のインストールに必要なネットワーク コンポーネントまで削除できない**RequiredAll**削除自体が。

 

たとえば場合は、INF ファイルをコンポーネント A を指定します、を通じて**RequiredAll**コンポーネント A が削除されるまで、コンポーネントのコンポーネント B B への依存関係を削除できません。 **RequiredAll**そのため、別のネットワーク コンポーネントの操作のために絶対に必要なネットワーク コンポーネントのみをインストールする必要があります。 たとえば、Net のコンポーネントに対して、INF ファイルの場合 (アダプター) が使用されます。 **RequiredAll** TCP/IP をインストールする必要がありますを指定する、ユーザーはできませんをそのアダプターが削除されるまでは、TCP/IP を削除します。 アダプターの INF を使用する必要があります、アダプターは TCP/IP 動作を必要としないため、 **RequiredAll** TCP/IP で依存関係を指定します。

INF ファイルを指定する、 **RequiredAll**依存関係が必要なネットワーク コンポーネントの INF ファイルが inf ディレクトリに存在することを確認する必要があります。 通常、これを実行、 **CopyINF**ディレクティブ。 詳細については、 **CopyINF**ディレクティブを参照してください[ **INF CopyINF ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyinf-directive)します。 INF ファイルをコピーする方法の詳細については、次を参照してください。[コピー Inf](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)します。

ネットワーク コンポーネントのインストールがで指定された場合、 **RequiredAll**エントリが失敗した場合は、指定したコンポーネントがも失敗したが必要なネットワーク コンポーネントのインストール。

 

 





