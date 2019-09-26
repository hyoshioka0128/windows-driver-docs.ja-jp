---
title: HTTP シンボル ストア
description: HTTP シンボル ストア
ms.assetid: b7dd1f3c-0135-4b69-9d70-b7cbf37fa969
keywords:
- HTTP シンボルストア
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81c51447b8dc2b4c5b1dd2ec640774556d9976ea
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284896"
---
# <a name="http-symbol-stores"></a>HTTP シンボル ストア


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


(デバッガーに付属している) symsrv でサポートされている SRV プロトコルを使用することにより、シンボルストアには HTTP (UNC/SMB のみではなく) を使用してアクセスできます。

HTTP は、ファイアウォールがクライアントとサーバー間で SMB を許可しない場合、SMB の代わりに一般的に使用されます。 実稼働環境とラボ環境は、この例の好例です。

HTTP シンボルサーバーは、読み取り専用の性質により、シンボルパスチェーンの下流ストアにすることはできません。 シンボルサーバープロキシ (ISAPI フィルター) は、この制限を回避します。 SymProxy は、事前に構成されたアップストリームシンボルストアを使用して、不足しているファイルをサーバーのファイルシステムにダウンロードします。 フィルターはファイルをファイルシステムにダウンロードします。これにより、IIS はファイルをクライアントにダウンロードできるようになり、シンボルストアチェーンの概念が復元されます。 詳細については、「 [Symproxy](symproxy.md) 」を参照してください。

シンボルファイルは静的ファイルとして提供されるだけなので、IIS をシンボルストアとして構成するのは比較的簡単です。 既定以外の設定では、バイナリストリームとしてシンボルファイルをダウンロードできるように、MIME の種類を構成します。 これを行うには、シンボルフォルダー\*の仮想ディレクトリに適用される "" ワイルドカードを使用します。

シンボルストアにインターネット経由でアクセスできるようにするには、シンボルファイルが格納されているディレクトリとインターネットインフォメーションサービス (IIS) の両方を構成する必要があります。

**注シンボルファイル**を提供するように IIS を構成する方法により、同じサーバーインスタンスを他の目的で使用することはお勧めしません。   通常、シンボルサーバーに必要なセキュリティ設定は、外部に接続されている商用サーバーなど、他の用途には適していません。 ここで説明するサンプル構成が環境に適していることを確認し、特定のニーズに合わせて調整します。

 

### <a name="span-idconfiguring_the_directoriesspanspan-idconfiguring_the_directoriesspancreating-the-symbol-directory"></a><span id="configuring_the_directories"></span><span id="CONFIGURING_THE_DIRECTORIES"></span>シンボルディレクトリの作成

まず、シンボルストアとして使用するディレクトリを選択します。 この例では、このディレクトリ c:\\symstore を呼び出し、ネットワーク上のサーバーの名前は\\symmachinename です。

シンボルストアを設定する方法の詳細については、「 [SymStore](symstore.md) And [Symbol store Folder Tree](symbol-store-folder-tree.md)」を参照してください。

### <a name="span-idconfiguring_iisspanspan-idconfiguring_iisspanconfiguring-iis"></a><span id="configuring_iis"></span><span id="CONFIGURING_IIS"></span>IIS の構成

仮想ディレクトリを作成し、MIME の種類を構成することにより、シンボルを提供するようにインターネットインフォメーションサービス (IIS) を構成する必要があります。 この処理が完了したら、認証方法を選択できます。

**仮想ディレクトリを作成するには**

1.  **[管理ツール]** から**インターネットインフォメーションサービス (IIS) マネージャー**を開きます。

2.  **[Web サイト]** に移動します。

3.  既定の **[Web サイト]** または使用中のサイトの名前を右クリックし、 **[仮想ディレクトリの追加]** を選択します。

4.  **エイリアス**の**シンボル**を入力し、 **[次へ]** をクリックします。

    管理を容易にするために、フォルダー、共有、および仮想ディレクトリに同じ名前を使用することをお勧めします。

5.  **パス**として **「c\\: SymStore** 」と入力し、 **[次へ]** をクリックします。

6.  **[OK]** をクリックして、仮想ディレクトリの追加を完了します。

サーバーに対して、サブディレクトリの構成プロセスを1回実行します。 これはグローバル設定であり、サイトのルートフォルダーでホストされていないアプリケーションに影響することに注意してください。

**サブディレクトリの構成**

1.  [  **\[コンピューター]に移動します。\]**

2.  **構成エディター**を開きます。

3.  システム ApplicationHost、**サイト** の順に移動します。

4.  **[Virtualdirectorydefaults]** を展開します。

5.  **Allowsubdirconfig**を*False*に設定します。

サーバーに対してこのプロセスを1回実行します。 これはグローバル設定であり、サイトのルートフォルダーでホストされていないアプリケーションに影響することに注意してください。

**記録シンボルファイルをブラウズ可能にする**

1.  [  **\[コンピューター]に移動します。\]サイト |\[Web サイト\] |シンボル**。

2.  中央のウィンドウで **[ディレクトリの参照]** をダブルクリックします。

3.  右側のウィンドウで **[有効化]** をクリックします。

ダウンロードしたコンテンツの MIME の種類は、IIS によってすべてのシンボルファイルが配信されるように、アプリケーション/オクテットストリームに設定する必要があります。

**MIME の種類の構成**

1. **[シンボル]** 仮想ディレクトリを右クリックし、 **[プロパティ]** を選択します。

2. **[HTTP ヘッダー]** を選択します。

3. **[MIME の種類]** をクリックします。

4. **[新規]** をクリックします。

5. **[拡張子]** に **\*** 「」と入力します。

6. **[MIME の種類]** に「 **application/オクテット-stream**」と入力します。

7. MIME の **[種類]** ダイアログボックスを閉じるには、 **[OK]** をクリックします。

8. シンボルの**プロパティ**を終了するには、[ **OK]** をクリックします。

Web.config ファイルを編集して、シンボルの MIME の種類を構成できます。 この方法では、継承された mime の種類をクリアし\* 、すべてのワイルドカードの mime の種類を追加します。 この方法は、特定の IIS 構成で MIME の種類が継承されている場合に必要になることがあります。

**Web.config を使用して MIME の種類を構成する**

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

これで、シンボルストアのすべての型のシンボルファイルを IIS で使用できるようになりました。

## <a name="span-idconfiguring_authenticationspanspan-idconfiguring_authenticationspanspan-idconfiguring_authenticationspanconfiguring-authentication"></a><span id="Configuring_Authentication"></span><span id="configuring_authentication"></span><span id="CONFIGURING_AUTHENTICATION"></span>認証の構成


"統合 Windows 認証" を使用するように IIS を構成することができます。これにより、エンドユーザーに資格情報の入力を求めることなく、クライアント (windbg など) が自動的に IIS に対して認証できるようになります。

**注:**   環境に適している場合は、シンボルサーバーへのアクセスを制御するように IIS で Windows 認証を構成するだけです。 環境に必要な場合は、IIS へのアクセスをさらに制御するために使用できるセキュリティオプションが他にもあります。

 

**認証方法を匿名として構成するには**

1.  **インターネットインフォメーションサービス (IIS) マネージャー**を起動します。

2.  [  **\[コンピューター]に移動します。\]サイト |\[Web サイト\] |シンボル**。

3.  中央のウィンドウで **[認証]** をダブルクリックします。

4.  **[認証とアクセス制御]** で、 **[編集]** をクリックします。

5.  **[Windows 認証]** を右クリックし、 **[有効にする]** を選択します。

6.  他のすべての認証プロバイダーについては、各プロバイダーを右クリックし、 **[無効化]** を選択します。

7.  **[OK]** をクリックして、認証の構成を完了します。

ウィンドウ認証が表示されない場合は、 **[Windows の機能の有効化または無効化**] を使用してこの機能を有効にします。 この機能の場所は、Windows のバージョンによって異なります。 Windows 8.1/Windows 2012 R2 では、インターネットインフォメーションサービス | の下にあります。World Wide Web Services |保護.

## <a name="span-iddisable_kerberos_supportspanspan-iddisable_kerberos_supportspanspan-iddisable_kerberos_supportspandisable-kerberos-support"></a><span id="Disable_Kerberos_Support"></span><span id="disable_kerberos_support"></span><span id="DISABLE_KERBEROS_SUPPORT"></span>Kerberos サポートを無効にする


IIS に接続する場合、SymSrv は Kerberos 認証をサポートしていません。 そのため、IIS で Kerberos 認証を無効にし、NTLM を唯一の Windows 認証プロトコルとして設定する必要があります。

**ご使用**の環境に適している場合にのみ、Kerberosセキュリティを無効にしてください。  

 

**Appcmd.exe を使用して Kerberos サポートを無効にする**

1.  コマンドプロンプトウィンドウを開く

2.  Kerberos を無効にし、NTLM を強制的に使用するには、次のコマンドを使用します。

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='NTLM']" /commit:apphost
    ```

3.  Kerberos が有効になっている既定値に戻すには、次のコマンドを使用します。

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='Negotiate,NTLM']" /commit:apphost
    ```

## <a name="span-idconfiguring_symsrv_client_authentication_promptsspanspan-idconfiguring_symsrv_client_authentication_promptsspanspan-idconfiguring_symsrv_client_authentication_promptsspanconfiguring-symsrv-client-authentication-prompts"></a><span id="Configuring_SymSrv_Client_Authentication_Prompts"></span><span id="configuring_symsrv_client_authentication_prompts"></span><span id="CONFIGURING_SYMSRV_CLIENT_AUTHENTICATION_PROMPTS"></span>SymSrv クライアント認証プロンプトの構成


SymSrv が認証要求を受信すると、デバッガーは認証ダイアログボックスを表示するか、構成方法に応じて自動的に要求を拒否することができます。 この動作は、! sym プロンプト on | off を使用して構成できます。 たとえば、プロンプトをオンにするには、次のコマンドを使用します。

```dbgcmd
!sym prompts on
```

現在の設定を確認するには、次のコマンドを使用します。

```dbgcmd
!sym prompts
```

詳細については[ **、「」を参照して**](-sym.md)[ください。](firewalls-and-proxy-servers.md)

 

 





