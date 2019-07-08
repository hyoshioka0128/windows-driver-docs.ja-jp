---
title: HTTP シンボル ストア
description: HTTP シンボル ストア
ms.assetid: b7dd1f3c-0135-4b69-9d70-b7cbf37fa969
keywords:
- シンボル ストアの HTTP
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b439221eabe7addb4a0221a2ac010d219631bb89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379142"
---
# <a name="http-symbol-stores"></a>HTTP シンボル ストア


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


Symsrv.dll (デバッガーに付属) でサポートされている SRV プロトコルを使用すると、シンボル ストアを (単なる UNC/SMB) ではなく HTTP を使用してアクセスできます。

ファイアウォールでは、クライアントとサーバー間で SMB ができない場合は、SMB ではなく HTTP が使用されます。 運用環境とラボ環境は、その良い例です。

HTTP のシンボル サーバーは、その読み取り専用の性質により、シンボル パスのチェーンのダウン ストリームのストアにすることはできません。 シンボル サーバー プロキシ (ISAPI フィルター) は、この制限を回避は機能します。 SymProxy は、アップ ストリームの事前構成済みのシンボル ストアを使用して、サーバーのファイル システムに不足しているファイルをダウンロードします。 フィルターは、IIS がシンボル ストアの組み合わせの概念を復元できるため、クライアントにファイルをダウンロードできるように、ファイル システムにファイルをダウンロードします。 参照してください[SymProxy](symproxy.md)詳細についてはします。

シンボル ストアとして IIS を構成するは静的ファイルとしてのみ提供されるファイルのシンボルとしては比較的簡単です。 のみ既定ではない設定は、バイナリ ストリームとしてシンボル ファイルのダウンロードを許可する MIME の種類の構成です。 これを行うを使用して、"\*"ワイルドカード シンボル フォルダーの仮想ディレクトリに適用します。

シンボル ストアをインターネット経由でアクセスできるようにするためにシンボル ファイルとインターネット インフォメーション サービス (IIS) を含む、両方のディレクトリを構成する必要があります。

**注**  IIS はシンボル ファイルを処理するために構成する方法のためには使用しないで、他の目的、同じサーバー インスタンスを使用することです。 通常、シンボル サーバーの必要なセキュリティ設定意味のないの他の使用などの外部に公開された commerce server。 ここで説明したサンプルの構成は、環境に適した、いることを確認し、特定のニーズに合わせて調整します。

 

### <a name="span-idconfiguringthedirectoriesspanspan-idconfiguringthedirectoriesspancreating-the-symbol-directory"></a><span id="configuring_the_directories"></span><span id="CONFIGURING_THE_DIRECTORIES"></span>シンボルのディレクトリを作成します。

シンボル ストアとして使用するディレクトリを選択して開始します。 この例でこのディレクトリの c: を呼び出して\\symstore、ネットワーク上のサーバーの名前が\\SymMachineName します。

シンボル ストアを設定する方法の詳細については、次を参照してください。 [SymStore](symstore.md)と[シンボルを格納フォルダー ツリー](symbol-store-folder-tree.md)します。

### <a name="span-idconfiguringiisspanspan-idconfiguringiisspanconfiguring-iis"></a><span id="configuring_iis"></span><span id="CONFIGURING_IIS"></span>IIS の構成

インターネット インフォメーション サービス (IIS) は、仮想ディレクトリを作成および MIME の種類を構成して、シンボルを提供するように構成する必要があります。 これを実行した後に認証方法を選択することができます。

**仮想ディレクトリを作成するには**

1.  **管理ツール**開く**インターネット インフォメーション サービス (IIS) マネージャー**します。

2.  移動します**Websites**します。

3.  右クリックして**既定の Web サイト**サイトの名前が使用されていると、選択または**仮想ディレクトリの追加.** .

4.  型**シンボル**の**エイリアス** をクリック**次**します。

    管理の容易さ、フォルダー、共有、および仮想ディレクトリの同じ名前を使用することをお勧めします。

5.  **パス**入力**c:\\SymStore**  をクリック**次**します。

6.  クリックして**OK**仮想ディレクトリの追加を完了します。

サーバーのサブディレクトリの構成プロセスを 1 回実行します。 これはグローバル設定で、サイトのルート フォルダーでホストされていないアプリケーションは、影響に注意してください。

**サブディレクトリの構成**

1.  移動します **\[コンピューター\]** します。

2.  開く、**構成エディター**します。

3.  移動します**システム ApplicationHost/サイト**します。

4.  展開**virtualDirectoryDefaults**します。

5.  設定**allowSubDirConfig**に*False*します。

サーバーのこのプロセスを 1 回実行します。 これはグローバル設定で、サイトのルート フォルダーでホストされていないアプリケーションは、影響に注意してください。

**任意の作成、シンボルが参照可能なファイルします。**

1.  移動します **\[コンピューター\] |サイト |\[Web サイト\]|シンボル**します。

2.  ダブルクリック**ディレクトリの参照**中央のウィンドウにします。

3.  クリックして**を有効にする**右側のペインでします。

ダウンロードしたコンテンツの MIME の種類は、IIS によって配信されるすべてのシンボル ファイルを許可するアプリケーションまたはオクテット ストリームに設定する必要があります。

**MIME の種類の構成**

1. 右クリックし、**シンボル**仮想ディレクトリを選択および**プロパティ**します。

2. 選択**HTTP ヘッダー**します。

3. クリックして**MIME の種類**します。

4. **[新規]** をクリックします。

5. **拡張子**、型 * *\\* * *。

6. **MIME の種類**、型**アプリケーションまたはオクテット ストリーム**します。

7. 終了する、 **MIME の種類**ダイアログ ボックスで、をクリックして**OK**。

8. 終了する**シンボル プロパティ**、 をクリックして**OK**します。

シンボルの MIME の種類を構成する web.config ファイルを編集することができます。 このアプローチは、継承された MIME の種類をクリアし、包括的なワイルドカードを追加します。 \* MIME の種類。 このアプローチは、特定の IIS 構成では、MIME の種類を継承しているときに、必要なことがあります。

**Web.config を使用して、MIME の種類を構成するには**

1.  次に示すように、web.config ファイルを編集します。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <system.webServer>
            <directoryBrowse enabled="true" />
            <staticContent>
                <clear />
                <mimeMap fileExtension=".*" 
    mimeType="application/octet-stream" />
            </staticContent>
        </system.webServer>
    </configuration>
    ```

2.  IIS を再起動します。

IIS は、すべてのシンボル ストアの種類のシンボル ファイルを処理する準備ができました。

## <a name="span-idconfiguringauthenticationspanspan-idconfiguringauthenticationspanspan-idconfiguringauthenticationspanconfiguring-authentication"></a><span id="Configuring_Authentication"></span><span id="configuring_authentication"></span><span id="CONFIGURING_AUTHENTICATION"></span>認証を構成します。


資格情報のエンドユーザーにメッセージを表示せず、クライアント (たとえば windbg.exe) は IIS に対して認証に自動的にできるように、「統合 Windows 認証」を使用するように IIS を構成することになります。

**注**  のみ環境に適している場合は、シンボル サーバーへのアクセスを制御するように IIS で Windows 認証を構成します。 お客様の環境に必要な場合は、IIS への他のセキュリティ オプションをさらに使用可能なコントロール アクセスがあります。

 

**匿名での認証方法を構成するには**

1.  起動、**インターネット インフォメーション サービス (IIS) マネージャー**します。

2.  移動します **\[コンピューター\] |サイト |\[Web サイト\]|シンボル**します。

3.  ダブルクリック**認証**中央のウィンドウにします。

4.  **認証とアクセス制御**クリックして**編集**します。

5.  右クリックして**Windows 認証**選択**を有効にする**します。

6.  その他のすべての認証プロバイダーの各プロバイダーを右クリックし、選択**を無効にする**します。

7.  クリックして**OK**認証の構成を完了します。

認証のウィンドウが表示されない場合は、使用**有効にする Windows 機能のオンとオフを**機能を有効にします。 機能の場所は、Windows のバージョンごとに異なります。 インターネット インフォメーション サービスでは、Windows 8.1/Windows 2012 R2、配置が |World Wide Web サービス |セキュリティ。

## <a name="span-iddisablekerberossupportspanspan-iddisablekerberossupportspanspan-iddisablekerberossupportspandisable-kerberos-support"></a><span id="Disable_Kerberos_Support"></span><span id="disable_kerberos_support"></span><span id="DISABLE_KERBEROS_SUPPORT"></span>Kerberos のサポートを無効にします。


SymSrv.dll は、IIS に接続するときは、Kerberos 認証をサポートしません。 そのため、Kerberos 認証は、唯一の Windows 認証プロトコルとして設定する、IIS と NTLM のニーズに無効にする必要があります。

**注**  環境に適している場合のみ Kerberos セキュリティを無効にします。

 

**Appcmd.exe を使用して Kerberos のサポートを無効にします。**

1.  コマンド プロンプト ウィンドウを開く

2.  で Kerberos を無効にして、NTLM の使用を強制するには、このコマンドを使用します。

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='NTLM']" /commit:apphost
    ```

3.  Kerberos が有効になっていると、既定値を返すには、するには、このコマンドを使用します。

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='Negotiate,NTLM']" /commit:apphost
    ```

## <a name="span-idconfiguringsymsrvclientauthenticationpromptsspanspan-idconfiguringsymsrvclientauthenticationpromptsspanspan-idconfiguringsymsrvclientauthenticationpromptsspanconfiguring-symsrv-client-authentication-prompts"></a><span id="Configuring_SymSrv_Client_Authentication_Prompts"></span><span id="configuring_symsrv_client_authentication_prompts"></span><span id="CONFIGURING_SYMSRV_CLIENT_AUTHENTICATION_PROMPTS"></span>SymSrv クライアント認証を構成するように求められます


SymSrv では、認証要求を受信するとデバッガーする認証 ダイアログ ボックスを表示するか自動的に構成した方法に応じて、要求を拒否します。 使用してこの動作を構成することができます。 sym は、で求める | オフ。 画面の指示を有効にする例では、このコマンドを使用します。

```dbgcmd
!sym prompts on
```

現在の設定を確認するには、このコマンドを使用します。

```dbgcmd
!sym prompts
```

詳細については、次を参照してください。 [ **! sym** ](-sym.md)と[ファイアウォールとプロキシ サーバー](firewalls-and-proxy-servers.md)します。

 

 





