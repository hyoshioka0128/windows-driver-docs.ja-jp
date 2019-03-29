---
title: クロス マシンの実行
description: クロス マシンの実行
ms.assetid: FDDD2320-E853-45a8-9820-12FB16365B9C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65d90e3dc148cef086aadbe67a89bff47e7a234
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580447"
---
# <a name="cross-machine-execution"></a>クロス マシンの実行


TAEF は、Te.exe 1 つのマシンで実行されますが、別のコンピューターでテストを実行する機能をサポートしています。 TAEF で認証し承認、テストを実行するために必要なバイナリを展開し、元のコンソールに戻り、すべての情報を記録します。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


次の要件はリモートでテストを実行するために必要です。

-   インストールして実行する必要があります[Te.Service](te-service.md) (x86 または x64) に **、ターゲット マシン**します。

### <a name="span-idexecutingwithdomainaccountsspanspan-idexecutingwithdomainaccountsspanspan-idexecutingwithdomainaccountsspanexecuting-with-domain-accounts"></a><span id="Executing_with_domain_accounts"></span><span id="executing_with_domain_accounts"></span><span id="EXECUTING_WITH_DOMAIN_ACCOUNTS"></span>ドメイン アカウントで実行します。

-   ドメイン アカウントは、管理者またはターゲット コンピューターのローカルの"リモート TAEF Users"グループのメンバーである必要があります。

### <a name="span-idexecutingwithnon-domainaccountsspanspan-idexecutingwithnon-domainaccountsspanspan-idexecutingwithnon-domainaccountsspanexecuting-with-non-domain-accounts"></a><span id="Executing_with_non-domain_accounts"></span><span id="executing_with_non-domain_accounts"></span><span id="EXECUTING_WITH_NON-DOMAIN_ACCOUNTS"></span>非ドメイン アカウントで実行します。

-   同じユーザー名とパスワードの両方のコンピューター上でローカル (非ドメイン アカウント) が存在する必要があります。
-   そのユーザーは、ターゲット コンピューターのローカルの"リモート TAEF Users"グループのメンバーである必要があります。
-   ホスト コンピューターには、Te.exe を実行できるローカル ユーザーまたは、または、ローカル ユーザーの汎用的な資格情報を資格情報マネージャーに追加することがあります。

    ``` syntax
    cmdkey /generic:<targetmachine> /user:<user_name> /pass:<password>
    ```

-   ドメインに参加しているコンピューターで実行している場合、ドメインに参加しているコンピューターは IPSec 境界除外が必要です。

## <a name="span-idexecutingtestsremotelyspanspan-idexecutingtestsremotelyspanspan-idexecutingtestsremotelyspanexecuting-tests-remotely"></a><span id="Executing_Tests_Remotely"></span><span id="executing_tests_remotely"></span><span id="EXECUTING_TESTS_REMOTELY"></span>テストをリモートで実行する.


### <a name="span-idrunonspanspan-idrunonspanspan-idrunonspanrunon"></a><span id="_runOn_"></span><span id="_runon_"></span><span id="_RUNON_"></span>/runOn:

テストをリモートで実行するために指定する必要があります、 **/runOn:&lt;マシン名&gt;** Te.exe とコマンドの残りのパラメーター。 前提条件を満たしている場合、ユーザー エクスペリエンスの残りの部分をローカルでテストを実行するときに同じになります。 すべてのログ出力を保存/書き込む、ローカル コンピューターにします。

以下に例を示します。

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1
```

-   ターゲット コンピューター (TAEFTest1) にテストのために必要なすべてのバイナリを送信し、コンソールにログインするときの wex.common.tests.dll 内に存在するすべての TAEF テストをリモートで実行します。

HRESULT 0x800706BA により、リモート マシンへの接続に失敗して、コンピューター名のスペルが正しいことを確認したら場合、マシンの IP アドレスを使用するかを使用して、 **/disableTimeouts**スイッチします。 接続の試行がタイムアウトする原因となりうる DNS 遅延があります。

**注:** 場合、これは、最初の時間を指定する、 **/runOn:** コマンドをクリックする必要があります**ブロック解除**Te.exe のファイアウォールの除外 ダイアログ ボックスでします。

### <a name="span-idtestdependenciesspanspan-idtestdependenciesspanspan-idtestdependenciesspantest-dependencies"></a><span id="Test_Dependencies"></span><span id="test_dependencies"></span><span id="TEST_DEPENDENCIES"></span>テストの依存関係

Te.exe は自動的にすべてのテストのネイティブおよびマネージ モジュールの依存関係を判別して、テスト dll と共にリモート コンピューターに送信します。 これは含まれません*システム*バイナリとすべての COM ライブラリ、テストが必要ですが。

使用して追加のテストの依存関係を手動で指定することができます、 **/TestDependencies**をコピーするファイルまたはディレクトリのセミコロン区切りのリストの形式でコマンド ライン パラメーターです。

- **[ファイル]**

  各ファイルの仕様は、ワイルドカード文字を含めることができます (test.txt; テスト\*.dll; など。)。 例:

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:*verification*.jpg;mysample.txt
  ```
  -   テストに TAEFTest1 だけでなく、任意のファイルで指定されたファイルに一致するすべての必要なバイナリを送信、 **/TestDependencies**パラメーター。
- **ディレクトリ**

  TAEF が存在するディレクトリの再帰的なディレクトリ検索をサポートしている*以下で*テスト バイナリを格納するディレクトリ。 以下に例を示します。

  ``` syntax
  te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\...
  ```

  -   TAEFTest1 と同様、すべてのファイル/ディレクトリ内、または下に、テストのために必要なすべてのバイナリ送信、 *unittests*ディレクトリ。 TAEF は、ディレクトリ階層を保持します。

  ``` syntax
  _    te unittests\wex.common.tests.dll /runon:TAEFTest1 /TestDependencies:unittests\*.jpg...
  ```

  -   TAEFTest1 と同様、すべての jpg ファイル内で以下に、テストのために必要なすべてのバイナリ送信、 *unittests*ディレクトリ。 TAEF は、ディレクトリ階層を保持します。

  <strong>注:</strong>存在しないディレクトリの再帰的または非再帰的なディレクトリ検索を指定する場合*以下で*test ディレクトリは、すべてのファイルは、リモート コンピューターにコピーされますが、ディレクトリ階層になりますフラット化されます。

Aso ことができますを使用して、テストの依存関係を指定[DeploymentItem メタデータ](deploymentitem-metadata.md)

## <a name="user-context"></a>ユーザー コンテキスト 


既定では、TAEF は自身のユーザー コンテキストを使用して、リモート マシンでテストを実行しようとします。 これはによって。

-   リモート コンピューター上のすべてのアクティブなセッションの列挙とを所有しているセッションを検索します。
    -   TAEF には、リモート コンピューターを所有しているセッションが検出されると、(そのデスクトップなど) でそのセッションで、テストを実行します。

        **注:** コンソール セッション必ずしも必要はありません。 リモート デスクトップ セッションが考えられます。

    -   場合 TAEF**見つからない**が所有しているリモート コンピューターでは、テストを実行、ログインしているユーザーとしてコンソール セッションに (そのデスクトップなど) 上のセッション。
    -   最後に、リモート コンピューター上のセッションを所有していない、コンソール セッションにログインしていない場合は、TAEF はテストを実行、セッション 0 で (非対話型)。

### <a name="span-idrunasspanspan-idrunasspanspan-idrunasspanrunas"></a><span id="RunAs"></span><span id="runas"></span><span id="RUNAS"></span>RunAs

指定した場合、 [/runAs](runas.md)に加えて値 **/runOn**、TAEF はそれらを満たすために必要な上記のヒューリスティックを使用して、 **/runAs**設定します。 例:

``` syntax
te unittests\wex.common.tests.dll /runon:TAEFTest1 /runas:system
```

-   システム アカウントで TAEFTest1 で wex.common.tests.dll 内に存在するすべての TAEF テストを実行します。

## <a name="span-idhowitworksspanspan-idhowitworksspanspan-idhowitworksspanhow-it-works"></a><span id="How_It_Works"></span><span id="how_it_works"></span><span id="HOW_IT_WORKS"></span>しくみ


-   Te.exe がリモート コンピューターで実行されている Te.Service のインスタンスに接続します。
    -   Windows 認証 (ネゴシエート) は、Te.Service を認証します。
    -   Te.Service では、管理者またはリモート コンピューター上のローカル"リモート TAEF Users"グループのメンバーがいることを確認して承認します。
-   Te.Service の下にディレクトリを作成します*RemoteTests*、テスト dll と同じ名前でします。
-   Te.exe では、リモート コンピューターでテストを実行するために必要なファイルのリストを構築します。 この一覧は次のとおりです。
    -   必要な TAEF バイナリ
    -   ネイティブまたはマネージ バイナリのすべての依存 (システム バイナリを除く)、テスト dll
    -   指定されている追加のファイル、 **/TestDependencies**パラメーター
-   Te.exe は、Te.Service に、各ファイルの Crc と共に、テストの依存関係のリストを送信します。
-   Te.Service では、リモート コンピューター上の各ファイルを検索し、CRC 値を比較します。 一覧から削除すると、および一覧は、クライアントに送信します。
-   依存関係の一覧内の残りのすべてのファイルがある場合は、Te.exe によって各依存関係が Te.Service に送信します。
    -   Te.Service で保存します、 &lt;Te.Service ディレクトリ&gt;\\RemoteTests\\&lt;テスト dll 名&gt;ディレクトリ。
-   Te.exe 確認、適切なを使用してリモート コンピューター上の新しい Te.ProcessHost.exe インスタンスを起動する Te.Service[ユーザー コンテキスト](#user-context)します。
-   Te.exe リモート Te.ProcessHost.exe インスタンスに接続し、テストの実行を開始します。

 

 





