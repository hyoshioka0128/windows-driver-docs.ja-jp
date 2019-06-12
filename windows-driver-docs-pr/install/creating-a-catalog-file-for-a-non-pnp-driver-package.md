---
title: 非 PnP ドライバー パッケージ用のカタログ ファイルの作成
description: 非 PnP ドライバー パッケージ用のカタログ ファイルの作成
ms.assetid: b40a6f42-53a8-468f-abf1-335c5ead3cbd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e301da648db48a14ae97b3635b3283a2687d350
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344336"
---
# <a name="creating-a-catalog-file-for-a-non-pnp-driver-package"></a>非 PnP ドライバー パッケージ用のカタログ ファイルの作成


使用することができます、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)を作成するツール、[カタログ ファイル](catalog-files.md)非 PnP の[ドライバー パッケージ](driver-packages.md)します。

**注**  INF ファイルを使用してインストールされていないドライバー パッケージのカタログ ファイルを作成するには、のみ MakeCat ツールを使用する必要があります。 INF ファイルを使用して、ドライバー パッケージをインストールする場合は、使用、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)カタログ ファイルを作成するためのツール。 Inf2Cat には、パッケージの INF ファイル内で参照される、ドライバー パッケージ内のすべてのファイルに自動的に含まれています。 Inf2Cat ツールを使用する方法の詳細については、次を参照してください。[カタログ ファイルを作成するのを使用して Inf2Cat](using-inf2cat-to-create-a-catalog-file.md)します。

 

カタログ ファイルを作成する必要がありますまず手動で作成するカタログの定義ファイル (.*します。cdf*) カタログ ヘッダー属性やファイルのエントリを説明します。 このファイルを作成すると、後に行うことができますし、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)カタログ ファイルを作成するためのツール

### <a name="creating-a-catalog-file"></a>カタログ ファイルを作成します。

非 PnP ドライバー パッケージのカタログ ファイルを作成するには、次の手順を実行します。

1.  テキスト エディターを使用して作成します。 *.cdf*ファイルの名前を一覧表示する、[カタログ ファイル](catalog-files.md)属性、およびカタログ ファイルで一覧表示するには、ファイルの名前は、作成します。

2.  使用して、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)カタログ ファイルを作成するコマンド ライン ツール。 MakeCat ツールの詳細については、次を参照してください。、[を使用して MakeCat](https://go.microsoft.com/fwlink/p/?linkid=70086) web サイト。

3.  ドライバーのインストール先のコンピューター上のカタログ ファイルをインストールします。

### <a name="overview-of-the-makecat-tool"></a>MakeCat ツールの概要

MakeCat ツールでは、次の処理時にします。 *.cdf*ファイル。

-   属性を検証、[カタログ ファイル](catalog-files.md)によって定義されている、。*します。cdf*ファイルを開き、カタログ ファイルに属性を追加します。

-   内に表示される各ファイルの属性を確認します。 *.cdf*ファイルを開き、カタログ ファイルに属性を追加します。

-   、暗号化ハッシュを生成または*拇印*、リスト内のファイルのそれぞれの。

-   カタログ ファイルでは、各ファイルの拇印を格納します。

カタログ ファイルを作成するのにには、次の MakeCat コマンドを使用します。

```cpp
MakeCat -v CatalogDefinitionFileName..cdf
```

各項目の意味は次のとおりです。

-   **-V**オプションを実行し、警告メッセージを印刷する MakeCat を構成します。

-   *CatalogDefinitionFileName.cdf*カタログ定義ファイルの名前を指定します。

### <a name="examples"></a>例

次の例は、Good という一般的なカタログ定義ファイルの内容を示しています.cdf。 カタログ化するパッケージには、2 つのファイルが含まれています。 *File1*と*File2*します。 結果として得られるカタログ ファイルの名前は Good.cat します。

```cpp
[CatalogHeader]
Name=Good.cat
PublicVersion=0x0000001
EncodingType=0x00010001
CATATTR1=0x10010001:OSAttr:2:6.0
[CatalogFiles]
<hash>File1=File1
<hash>File2=File2
```

この例で使用されるオプションは次のとおりです。 これらのオプションの詳細については、次を参照してください。、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922) web サイト。

<a href="" id="name-good-cat"></a>Name=Good.cat  
カタログ ファイルの名前を指定します (*Good.cat*)。

<a href="" id="publicversion-0x0000001"></a>PublicVersion=0x0000001  
カタログ ファイルのバージョンを指定します。

<a href="" id="encodingtype-0x00010001"></a>EncodingType=0x00010001  
エンコードの種類、サムプリントの生成に使用されるメッセージを指定します。 値 0x00010001 PKCS_7_ASN_ENCODING のエンコーディングの種類のメッセージを指定します |X509_ASN_ENCODING します。

<a href="" id="catattr1-0x10010001-osattr-2-6-0"></a>CATATTR1=0x10010001:OSAttr:2:6.0  
カタログ ファイルの属性を指定します。 追加の属性を指定するには、をサフィックスとして一意の数字が割り当てられている各オプションで別の CATATTR オプションを使用する必要があります。 たとえば、CATATT1 を使用して、1 つのカタログ ファイルの属性と指定する CATATT2 を指定します。

この例では、CATATTR1 オプションを使用して指定されている属性は、次の値を持ちます。

<a href="" id="0x10010001"></a>0x10010001  
次のように属性を指定します。

-   0x10000000 - 認証済みの属性 (署名、拇印に含まれる)。

-   0x00010000 - 属性は、プレーン テキストで表現されます。

-   0x00000001 - 属性は名前と値のペアです。

<a href="" id="osattr-2-6-0"></a>OSAttr:2:6.0  
OSAttr 属性を持つ署名の要件と互換性のあるターゲットの Windows バージョンを指定します、[ドライバー パッケージ](driver-packages.md)します。 属性の値では、次の項目を指定します。

-   値*2*カタログ ファイルが NT ベースのバージョンの Windows オペレーティング システムとの互換性を指定します。

-   値*6.0*カタログ ファイルが Windows Vista と互換性を指定します。
    **注**  場合、[ドライバー パッケージ](driver-packages.md)は複数の Windows バージョンと互換性のある、する必要がありますオプションを使用して個別 CATATTR OSAttr 属性を各 Windows バージョンを指定します。

     

<a href="" id="-hash-file1-file1"></a>&lt;ハッシュ&gt;File1 File1 を =  
File1、カタログ ファイルで参照されているファイルの参照のタグを指定します。 値 *&lt;ハッシュ&gt;File1*結果ファイルの暗号化ハッシュ、されているタグまたは*拇印*します。

<a href="" id="-hash-file1-file2"></a>&lt;ハッシュ&gt;File1 File2 を =  
カタログ ファイルで参照されている、File2、ファイルの参照のタグを指定します。 値 *&lt;ハッシュ&gt;File2*ファイルの拇印をされているタグになります。

次の例を生成する方法を示しています、[カタログ ファイル](catalog-files.md)、 *Good.cat、* 対応するカタログ定義ファイルから*良い.cdf*します。 Makecat 保存*Good.cat*同じフォルダーにいる*File1*と*File2*が配置されています。

```cpp
MakeCat -v Good.cdf
```

 

 





