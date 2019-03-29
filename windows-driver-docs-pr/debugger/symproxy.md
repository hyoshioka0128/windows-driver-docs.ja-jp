---
title: SymProxy
description: SymProxy
ms.assetid: c0b122fe-4996-4659-a3f1-95831605c0b3
keywords:
- シンボル、SymProxy (symproxy.dll)
- シンボル ストアでは、HTTP
- シンボル ストア、SymProxy (symproxy.dll)
- SymProxy
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca844e346e047ff43cc5bf4b79e28357a0bc933
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577864"
---
# <a name="symproxy"></a>SymProxy


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


クライアント コンピューターとその他のシンボル ストアの間のプロキシとして機能する、HTTP ベースのシンボル ストアを構成することができます。 実装は、SymProxy (Symproxy.dll) と呼ばれる Internet Server Application Programming Interface (ISAPI) フィルターです。 SymProxy サーバーは、インターネットまたは企業ネットワーク内の他のソースにゲートウェイ コンピューターとして使用できます。 次の図は、SymProxy 構成の例を示します。

![symproxy 構成の例の図](images/symproxy-configuration.png)

SymProxy は、多くの状況で便利です。 例:

-   これで、コンピューターに接続されていない、会社のネットワークをラボ環境内で多くのシステムをデバッグ中は、シンボルはネットワークに格納され、統合 Windows 認証 (IWA) を使用してアクセスする必要があります。

-   デバッグ中のコンピューターからインターネットにアクセスを防止するファイアウォールが、企業のコンピューティング環境に含まれています、インターネットの Web サイトからシンボルを取得する必要があります。

-   理解も、シンボルが存在すると、考慮する必要がありますがないように、社内のすべてのユーザーに対して 1 つのシンボル パスを表示して、ユーザーの介入なしの新しいシンボル ストアを追加することができます。

-   物理的に、会社のリソースの残りの部分から遠く離れたリモート サイトがあり、ネットワーク アクセスが遅い。 このシステムは、シンボルを取得し、リモート サイトへのキャッシュに使用できます。

SymProxy をインストールするにする必要があります手動でファイルの正しい場所にコピーします、レジストリを構成、ネットワークのセキュリティ資格情報を選択およびインターネット インフォメーション サービス (IIS) を構成します。 HTTP、シンボル ストアが正しく構成されていることを確認するを参照してください。 [HTTP シンボル ストア](http-symbol-stores.md)します。

### <a name="span-idmultiplesymbolserverperformanceconsiderationsspanspan-idmultiplesymbolserverperformanceconsiderationsspanspan-idmultiplesymbolserverperformanceconsiderationsspanmultiple-symbol-server-performance-considerations"></a><span id="Multiple_Symbol_Server_Performance_Considerations"></span><span id="multiple_symbol_server_performance_considerations"></span><span id="MULTIPLE_SYMBOL_SERVER_PERFORMANCE_CONSIDERATIONS"></span>複数のシンボル サーバー パフォーマンスの考慮事項

各仮想ディレクトリは、複数の (アップ ストリーム) シンボル ストアに関連付けることができます。 各シンボル ストアが個別に照会されます。 パフォーマンスは、SMB サーバーのローカルはインターネット HTTP サーバーの前に処理する必要があります。 デバッガー シンボルのパスとは異なり、SymProxy のシンボル パスに複数の HTTP シンボル ストアを指定できます。 1 つの仮想ディレクトリは、10 個のエントリの最大値がサポートされています。

### <a name="span-idsymproxysymbolpathspanspan-idsymproxysymbolpathspanspan-idsymproxysymbolpathspansymproxy-symbol-path"></a><span id="SymProxy_Symbol_Path"></span><span id="symproxy_symbol_path"></span><span id="SYMPROXY_SYMBOL_PATH"></span>SymProxy シンボル パス

SymProxy に分割されます (定義されているレジストリ) のシンボル パスの値の個々 のエントリを各エントリを使用して、SRV を生成する\*ベースのファイルを取得するシンボルのパス。 マージを単一のダウン ストリーム シンボル ストアのアップ ストリームのストアとして各ダウン ストリーム ストア、クエリの – 実際には、仮想ディレクトリのフォルダーを使用します。

SymProxy で使用される (生成) のシンボル パスは、これと同等です。

```dbgcmd
SRV*<Virtual Directory Folder>*<SymbolPath Entry #N>
```

この例で、UNC パスと 2 つの HTTP パスが、企業のシンボル サーバー、Microsoft およびサード パーティ (Contoso) からシンボルをマージする仮想ディレクトリに関連付けられます。 SymProxy SymbolPath は、次のように設定します。

```console
\\MainOffice\Symbols;https://msdl.microsoft.com/download/symbols;
https://symbols.contoso.com/symbols
```

メイン オフィスのシンボルのファイル共有を照会するには、最初の (生成) のシンボル パスを使用しています。

```dbgcmd
SRV*D:\SymStore\Symbols*\\MainOffice\Symbols
```

シンボル ファイルが見つからない場合の (生成) のシンボル パスを使用して Microsoft のシンボル ストアがクエリします。

```dbgcmd
SRV*D:\SymStore\Symbols*https://msdl.microsoft.com/download/symbols
```

ファイルがまだ見つからないかどうか、Contoso のシンボル ストア (https://symbols.contoso.com/symbols)の (生成) のシンボル パスを使用して、クエリを実行します。

```dbgcmd
SRV*D:\SymStore\Symbols*https://symbols.contoso.com/symbols
```

このセクションの内容:

[SymProxy をインストールします。](installing-symproxy.md)

[レジストリを構成します。](configuring-the-registry.md)

[ネットワーク セキュリティ資格情報を選択します。](choosing-network-security-credentials.md)

[IIS SymProxy の構成](configuring-iis-for-symproxy.md)

[除外リストを設定します。](setting-up-exclusion-lists.md)

[使用できないシンボル ストアを処理します。](dealing-with-unavailable-symbol-stores.md)

[ファイル ポインターの処理](handling-file-pointers.md)

[取得したシンボル ファイルのキャッシュ](caching-acquired-symbol-files.md)

 

 





