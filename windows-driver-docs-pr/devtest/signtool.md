---
title: SignTool
description: SignTool (Signtool.exe) は、CryptoAPI のコマンド ライン ツールをその署名をデジタル ファイルには、ファイル、および時刻のスタンプ ファイルの署名を検証します。
ms.assetid: c1006c07-f204-4fc0-8f99-36e69cbee96d
keywords:
- SignTool ドライバー開発ツール
topic_type:
- apiref
api_name:
- SignTool
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a5f655d962d532da1c51025c15848cfa49a887
ms.sourcegitcommit: 5bfb01d5aa52632b54182f3db87454df2d61cbe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2019
ms.locfileid: "56905511"
---
# <a name="signtool"></a>SignTool


SignTool (Signtool.exe) は、コマンド ライン[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)そのデジタル署名ファイルをツールで、ファイル、および時刻のスタンプ ファイルの署名を検証します。

```
    SignTool [Operation] [Options] [FileName ...]
```

### <a name="span-idpartiallistofoperationsswitchesandargumentsspanspan-idpartiallistofoperationsswitchesandargumentsspanpartial-list-of-operations-options-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、オプション、および引数の一覧の一部

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>操作

<span id="catdb"></span><span id="CATDB"></span>**catdb**  
カタログ データベースを更新する SignTool を構成します。 SignTool はカタログ ファイルをデータベースに追加するか、データベースからカタログを削除します。 既定で、 **catdb**コマンドでは、名前がで指定されたファイルを追加します。、 *FileName*システム コンポーネント (ドライバー) データベースへの引数。

**注**  カタログ ファイルの自動検索のカタログのデータベースを使用します。

 

<span id="sign"></span><span id="SIGN"></span>**サインイン**  
SignTool をデジタルへの署名をファイル名がで指定された構成、 *FileName*引数。

<span id="timestamp"></span><span id="TIMESTAMP"></span>**タイムスタンプ**  
名前がで指定されたファイルのタイムスタンプに SignTool を構成、 *FileName*引数。

<span id="verify"></span><span id="VERIFY"></span>**確認します**  
名前がで指定されたファイルのデジタル署名を検証する署名ツールの構成、 *FileName*引数。

### <a name="span-idcatdboperationswitchesspanspan-idcatdboperationswitchesspancatdb-operation-options"></a><span id="catdb_operation_switches"></span><span id="CATDB_OPERATION_SWITCHES"></span>Catdb 操作オプション

<span id="_d"></span><span id="_D"></span>**/d**  
カタログ データベースを更新する SignTool を構成します。 どちらの場合 **/d**も **/g**オプションを使用すると、SignTool がシステム コンポーネントおよびドライバー データベースを更新します。

<span id="_g_Guid"></span><span id="_g_guid"></span><span id="_G_GUID"></span>**/g** *Guid*  
によって識別されるカタログ データベースを更新する SignTool を構成、 *GUID*引数。

<span id="_r"></span><span id="_R"></span>**/r**  
SignTool ごとの名前を持つがで指定されたカタログ ファイルを削除する構成、 *FileName*カタログ データベースからの引数。 このオプションが指定されていない場合、SignTool はカタログ データベースに指定したカタログ ファイルを追加します。

<span id="_u"></span><span id="_U"></span>**/u**  
必要に応じて、カタログ データベースの既存のカタログ ファイルと、競合を避けるためにカタログ ファイルの一意の名前を生成する SignTool を構成します。 このオプションが指定されていない場合、SignTool は追加されるカタログと同じ名前を持つ既存のカタログを上書きします。

### <a name="span-idsignoperationswitchesspanspan-idsignoperationswitchesspansign-operation-options"></a><span id="sign_operation_switches"></span><span id="SIGN_OPERATION_SWITCHES"></span>サインイン操作のオプション

<span id="_a_"></span><span id="_A_"></span>**/a**   
SignTool を最適な署名証明書を自動的に選択を構成します。 このオプションが存在しない場合、SignTool は 1 つだけの署名証明書を検索する期待しています。

<span id="_ac_CrossCertFileName"></span><span id="_ac_crosscertfilename"></span><span id="_AC_CROSSCERTFILENAME"></span>**/ac** *CrossCertFileName*  
という名前のソフトウェア発行元証明書 (SPC) で使用されるクロス証明書ファイルの名前を示す*CertificateName*証明書ストアにインストールされている*StoreName*します。 このオプションは、署名証明書は、SPC 場合にのみ使用する必要があります。

<span id="_c_CertTemplateName"></span><span id="_c_certtemplatename"></span><span id="_C_CERTTEMPLATENAME"></span>**/c** *CertTemplateName*  
署名証明書の証明書テンプレート名 (Microsoft 拡張機能) を指定します。

<span id="_csp_CSPName"></span><span id="_csp_cspname"></span><span id="_CSP_CSPNAME"></span>**/csp** *CSPName*  
秘密キー コンテナーを含む暗号化サービス プロバイダー (CSP) を指定します。

<span id="_d_Desc"></span><span id="_d_desc"></span><span id="_D_DESC"></span>**/d** *Desc*  
署名されたコンテンツの説明を指定します。

<span id="_du_URL"></span><span id="_du_url"></span><span id="_DU_URL"></span>**/du** *URL*  
署名されたコンテンツの詳細な説明の URL を指定します。

<span id="_f_SignCertFile"></span><span id="_f_signcertfile"></span><span id="_F_SIGNCERTFILE"></span>**/f** *SignCertFile*  
ファイル内の署名証明書を指定します。 Personal Information Exchange (PFX) ファイル形式のみがサポートされています。 使用することができます、 [ **Pvk2Pfx** ](pvk2pfx.md) SPC と PVK を変換するツールのファイルを PFX 形式にします。

ファイルをパスワードで保護された PFX 形式の場合、使用、 **/p**パスワードを指定するオプション。 使用して、ファイルに秘密キーが含まれていない場合、 **/csp**と **/k** CSP および秘密キー コンテナーの名前をそれぞれ指定するオプション。

<span id="_fd"></span><span id="_FD"></span>**/fd**  
ファイルの署名を作成する際に使うファイル ダイジェスト アルゴリズムを指定します。 既定値には SHA1 です。

<span id="_i_IssuerName"></span><span id="_i_issuername"></span><span id="_I_ISSUERNAME"></span>**/i** *IssuerName*  
署名証明書の発行者の名前を指定します。 この値は、全体の発行者名の部分文字列を指定できます。

<span id="_j_DLL"></span><span id="_j_dll"></span><span id="_J_DLL"></span>**/j** *DLL*  
シグネチャの属性を提供する DLL の名前を指定します。

<span id="_jp_ParameterName"></span><span id="_jp_parametername"></span><span id="_JP_PARAMETERNAME"></span>**/jp** *ParameterName*  
指定された DLL に渡されるパラメーターを指定します、 **/j**コマンド。

<span id="_kc_PrivKeyContainerName"></span><span id="_kc_privkeycontainername"></span><span id="_KC_PRIVKEYCONTAINERNAME"></span>**/kc** *PrivKeyContainerName*  
秘密キーのキー コンテナー名を指定します。

<span id="_n_SubjectName"></span><span id="_n_subjectname"></span><span id="_N_SUBJECTNAME"></span>**/n** *SubjectName*  
署名証明書のサブジェクトの名前を指定します。 この値は、サブジェクト名の一部でもかまいません。

<span id="_nph"></span><span id="_NPH"></span>**/nph**  
サポートされている場合は、実行可能ファイルのページ ハッシュを抑制します。 既定値は、SIGNTOOL によって決まります\_ページ\_ハッシュ環境変数と wintrust.dll のバージョン。 このオプションでは、PE ファイル以外は無視されます。

<span id="_p_Password"></span><span id="_p_password"></span><span id="_P_PASSWORD"></span>**/p** *パスワード*  
PFX ファイルを開く時に使うパスワードを指定します 使用して、PFX ファイルを指定することができます、 **/f**オプション

<span id="_p7__Path"></span><span id="_p7__path"></span><span id="_P7__PATH"></span>**/p7** *Path*  
指定する公開キー暗号化標準 (PKCS)\#コンテンツ ファイルに指定された各の 7 のファイルが生成されます。 PKCS \#7 のファイルの名前はパス\\filename.p7 します。

<span id="_p7ce_Value"></span><span id="_p7ce_value"></span><span id="_P7CE_VALUE"></span>**/p7ce** *値*  
署名された PKCS のオプションを指定します\#7 のコンテンツ。 設定値を"Embedded"に、PKCS で署名されたコンテンツを埋め込む\#7 のファイルにデタッチされた PKCS の符号付きのデータ部分を作成するには"DetachedSignedData" \#7 のファイル。 場合、 **/p7ce**オプションが使用されない場合、既定で署名されたコンテンツが埋め込まれています。

<span id="_p7co__OID"></span><span id="_p7co__oid"></span><span id="_P7CO__OID"></span>**/p7co** *OID*  
署名された PKCS を識別するオブジェクト識別子 (OID) を指定します\#7 のコンテンツ。

<span id="_ph___"></span><span id="_PH___"></span>**/ph**   
でサポートされている場合は、実行可能ファイルのページ ハッシュを生成します。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span>**/r** *RootSubjectName*  
署名の証明書のチェーンする必要があります、ルート証明書のサブジェクト名を指定します。 この値は、ルート証明書の件名全体の部分文字列を指定できます。

<span id="_s_StoreName"></span><span id="_s_storename"></span><span id="_S_STORENAME"></span>**/s** *StoreName*  
ファイルの署名に使用する証明書を検索するときに開く証明書ストアの名前を指定します。 このオプションが指定されていない場合、**マイ**証明書ストアを開くことができます。

<span id="_sha1_Hash"></span><span id="_sha1_hash"></span><span id="_SHA1_HASH"></span>**/sha1** *Hash*  
署名証明書の SHA1 ハッシュを指定します。

<span id="_sm"></span><span id="_SM"></span>**/sm**  
ユーザーの証明書ストアではなく、コンピューター証明書ストアを使用する署名ツールを構成します。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span>**/t** *URL*  
タイムスタンプ サーバーの URL を指定します。 このオプションが指定されていない場合、署名済みファイルはこのタイムスタンプではありません。 カタログ ファイルまたはドライバーのファイルはタイムスタンプ、署名者のキーが侵害された場合、タイムスタンプは、ファイルの署名に使用されたキーを取り消すために必要な情報を提供するためです。

<span id="_td____alg"></span><span id="_TD____ALG"></span>**/td** *alg*  
RFC 3161 タイム スタンプ サーバーで使用されるダイジェスト アルゴリズムを要求する/tr オプションと共に使用します。

<span id="_tr___URL"></span><span id="_tr___url"></span><span id="_TR___URL"></span>**/tr** *URL*  
RFC 3161 タイム スタンプ サーバーの URL を指定します。 場合、このオプション (または **/t**) は、存在していない署名ファイルされますタイムスタンプ。 タイムスタンプが失敗した場合、警告が生成されます。 このオプションでは使用できません、 **/t**オプション。

<span id="_u___Usage"></span><span id="_u___usage"></span><span id="_U___USAGE"></span>**/u** *使用状況*  
拡張キー使用法 (EKU) 署名証明書に存在する必要があるを指定します。 使用法の値は、OID または文字列で指定できます。 既定の使用法は、"Code Signing"(1.3.6.1.5.5.7.3.3) です。

<span id="_uw_"></span><span id="_UW_"></span>**/uw**   
"Windows System Component Verification"(1.3.6.1.4.1.311.10.3.6) の使用量を指定します。

### <a name="span-idtimestampoperationswitchesspanspan-idtimestampoperationswitchesspantimestamp-operation-options"></a><span id="timestamp_operation_switches"></span><span id="TIMESTAMP_OPERATION_SWITCHES"></span>Timestamp 操作オプション

<span id="_p7_"></span><span id="_P7_"></span>**/p7**   
PKCS のタイムスタンプ\#7 ファイル。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span>**/t** *URL*  
タイムスタンプ サーバーの URL を指定します。 ファイルのタイムスタンプをされている必要がありますが署名されて以前

<span id="_td___alg"></span><span id="_TD___ALG"></span>**/td** *alg*  
RFC 3161 タイム スタンプ サーバーで使用されるダイジェスト アルゴリズムを要求します。 **/td**を併用、 **/tr**オプション。

<span id="_tp__index"></span><span id="_TP__INDEX"></span>**/tp** *index*  
インデックス位置にある署名をタイムスタンプします。

<span id="_tr___alg"></span><span id="_TR___ALG"></span>**/tr** *alg*  
RFC 3161 タイム スタンプ サーバーで使用されるダイジェスト アルゴリズムを要求します。 **/td**を併用、 **/tr**オプション。

### <a name="span-idverifyoperationswitchesspanspan-idverifyoperationswitchesspanverify-operation-options"></a><span id="verify_operation_switches"></span><span id="VERIFY_OPERATION_SWITCHES"></span>操作のオプションを確認します。

<span id="_a"></span><span id="_A"></span>**/a**  
すべてのメソッドをファイルの検証に使用できることを指定します。 最初に、カタログ データベースは、カタログのファイルが署名されているかどうかを判断する検索されます。 ファイルは、任意のカタログで署名されていない場合、SignTool は、ファイルの埋め込み署名を検証しようとします。 カタログで署名できない可能性がありますが、またはファイルを検証するときに、このオプションを使うことをお勧めします。

<span id="_ad"></span><span id="_AD"></span>**/ad**  
カタログで署名されたファイルの既定のカタログ データベースのみを検索することを指定します。

<span id="_all"></span><span id="_ALL"></span>**/all**  
複数の署名を含むファイル内のすべての署名を確認します。

<span id="_as"></span><span id="_AS"></span>**/as**  
カタログで署名されたファイルのシステム コンポーネント (ドライバー) カタログ データベースのみを検索することを指定します。

<span id="_ag_CatDBGUID"></span><span id="_ag_catdbguid"></span><span id="_AG_CATDBGUID"></span>**/ag** *CatDBGUID*  
データベースを指定だけである、カタログ、を介して識別される、 *CatDBGUID*カタログで署名されたファイルの引数が検索されます。

<span id="_c___CatalogFileName"></span><span id="_c___catalogfilename"></span><span id="_C___CATALOGFILENAME"></span>**/c** *CatalogFileName*  
カタログ ファイルの名前を指定します。

<span id="_d___"></span><span id="_D___"></span>**/d**   
署名ツールで、説明と説明の URL を印刷する必要があることを指定します。

<span id="_ds___index"></span><span id="_DS___INDEX"></span>**/ds** *index*  
指定した位置にある署名を確認します。

<span id="_hash__SHA1SHA256"></span><span id="_hash__sha1sha256"></span><span id="_HASH__SHA1SHA256"></span>**/hash** {**SHA1**|**SHA256**}  
カタログ内のファイルの検索に使用する省略可能なハッシュ アルゴリズムを指定します。

<span id="_kp"></span><span id="_KP"></span>**/kp**  
確認する署名ツールで指定されたファイルのデジタル署名を構成します、 *FileName*引数に準拠している、[カーネル モード コードの署名ポリシー](https://msdn.microsoft.com/library/windows/hardware/ff548231) 、 [PnP デバイスインストール要件を署名](https://msdn.microsoft.com/library/windows/hardware/ff549724)の Windows Vista および Windows の以降のバージョン。 このオプションが指定されていない場合、SignTool は署名が、PnP デバイス インストールの署名の要件に準拠しているだけ確認します。

<span id="_ms"></span><span id="_MS"></span>**/ms**  
複数の検証セマンティクスを使用します。 これは、既定の動作を[ **WinVerifyTrust 関数**](https://msdn.microsoft.com/library/windows/desktop/aa388208) Windows 8 以降を呼び出します。

<span id="_o_Version"></span><span id="_o_version"></span><span id="_O_VERSION"></span>**/o** *バージョン*  
オペレーティング システムのバージョンに従ってファイルを確認します。 形式、*バージョン*引数が<em>PlatformID</em>**:**<em>VerMajor</em>**.**<em>VerMinor</em>**.**<em>BuildNumber</em>

使用、 **/o**オプションはお勧めします。 場合 **/o**が指定されていない、SignTool は予期しない結果を返す可能性があります。 たとえば、含めないでください、 **/o**オプションでは、以前のオペレーティング システムで正しく検証されるシステム カタログがで正しく検証されない新しいオペレーティング システム。

<span id="_p7"></span><span id="_P7"></span>**/p7**  
PKCS のことを確認します。 \#7 ファイル。 PKCS の既存のポリシーは使用されません\#7 検証します。 署名が確認され、署名証明書のチェーンがビルドされます。

<span id="_pa"></span><span id="_PA"></span>**/pa**  
確認する署名ツールで指定されたファイルのデジタル署名を構成します、 *FileName*引数に準拠している、 [PnP デバイスのインストール要件を署名](https://msdn.microsoft.com/library/windows/hardware/ff549724)します。

**注**  でこのオプションは使用できません、 **catdb**オプション。

 

<span id="_pg__PolicyGUID"></span><span id="_pg__policyguid"></span><span id="_PG__POLICYGUID"></span>**/pg** *PolicyGUID*  
GUID により検証ポリシーを指定します。 PolicyGUID は、検証ポリシーの ActionID に対応します。

**注**  でこのオプションは使用できません、 **catdb**オプション。

 

<span id="_ph__"></span><span id="_PH__"></span>**/ph**   
署名ツールが印刷およびページ ハッシュ値を検証する必要がありますを指定します。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span>**/r** *RootSubjectName*  
署名の証明書のチェーンする必要があります、ルート証明書のサブジェクト名を指定します。 この値は、ルート証明書の件名全体の部分文字列を指定できます。

<span id="_tw"></span><span id="_TW"></span>**/tw**  
署名にタイムスタンプがない場合に警告が生成されることを指定します。

### <a name="span-idgeneralswitchesspanspan-idgeneralswitchesspangeneral-options"></a><span id="general_switches"></span><span id="GENERAL_SWITCHES"></span>全般オプション

<span id="_q"></span><span id="_Q"></span>**/q**  
正常に実行し、失敗した実行の最小限の出力に出力を表示 SignTool を構成しません。

<span id="_v"></span><span id="_V"></span>**/v**  
詳細な操作と警告メッセージのバージョンを表示する SignTool を構成します。

<span id="__"></span>**/?**  
SignTool がコマンド ウィンドウでヘルプ情報を表示するよう構成します。

<span id="FileName_..."></span><span id="filename_..."></span><span id="FILENAME_..."></span>*ファイル名には.*  
1 つまたは複数のファイル名の一覧を指定します。 に応じて、コマンドは、SignTool はサインインは、タイムスタンプ、または、指定されたファイルを確認します。 場合、 **catdb**コマンドを使用すると、SignTool は追加または指定したファイルをカタログ データベースから削除します。

**サインオン**、**タイムスタンプ**、および**ことを確認**コマンド、ファイルのカタログ ファイルであることができます、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)またはドライバー ファイル。

**Catdb**コマンド、ファイルのカタログ ファイルをする必要があります、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

SignTool は、多数のオプションをサポートします。 このトピックで説明するオプションは、署名や、ドライバー パッケージまたはドライバ ファイルの検証に使用できるものに制限されます。

SignTool パラメーターの完全な一覧は、Microsoft を参照してください。 [SignTool](https://go.microsoft.com/fwlink/p/?linkid=62661) web サイト。

ファイルへの署名の詳細については、Microsoft を参照してください。[暗号化ツール](https://go.microsoft.com/fwlink/p/?linkid=10637)web サイト。

SignTool の 32 ビット バージョンが、箱にある\\WDK の i386 フォルダー。 ツールの 64 ビット バージョンが、箱にある\\amd64 と bin\\WDK の ia64 フォルダー。

### <a name="span-idsigningexamplesspanspan-idsigningexamplesspansigning-examples"></a><span id="signing_examples"></span><span id="SIGNING_EXAMPLES"></span>署名の例

署名する方法の例を次に、[ドライバー パッケージの](https://msdn.microsoft.com/library/windows/hardware/ff544840)カタログ ファイルがソフトウェア発行元証明書 (SPC) と、対応するクロス証明書を使用します。 この例は、64 ビット バージョンの Windows Vista 以降のバージョンの Windows で、カーネル モード コードを署名ポリシーを適用するドライバー パッケージに署名するため無効です。 例では、ドライバー パッケージのカタログ ファイル AbcCatFileName.cat を署名します。 カタログ ファイルをサインインするには、例では、クロス証明書 AbcCrossCertificate と AbcSPCCertificate 証明書を使用します。 AbcSPCCertificate 証明書は、AbcCertificateStore 証明書ストアにあります。

例は、カタログ ファイルの署名にも、パブリックに利用可能なタイムスタンプ サーバーを使用します。 タイムスタンプ サーバーは VeriSign によって提供され、その URL が http://timestamp.verisign.com/scripts/timstamp.dllします。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll AbcCatFileName.cat
```

次は、SPC とクロス証明書を使用して、ドライバー ファイルに署名を埋め込む方法の例です。 すべてのパラメーターは、点を除いて、ファイルが署名されている AbcDriverFile.sys AbcCatFileName.cat カタログ ファイルではなく、カタログ ファイルに署名する例のように同じです。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll AbcDriverFile.sys
```

署名する方法の例を次に、[ドライバー パッケージの](https://msdn.microsoft.com/library/windows/hardware/ff544840)カタログ ファイルを使用して、[コマーシャル リリースの証明書](https://msdn.microsoft.com/library/windows/hardware/ff539935)または[市販のテスト証明書](https://msdn.microsoft.com/library/windows/hardware/ff539940)します。 この例は、Windows Vista の 32 ビット バージョン、以降のバージョンの Windows で、カーネル モード コード署名ポリシーを適用しないドライバー パッケージに署名するため無効です。 例では、ドライバー パッケージのカタログ ファイル CatalogFileName.cat を署名します。 カタログ ファイルの署名に、TestCertificateStore 証明書ストアにある、AbcTestCertificate テスト証明書を使用します。

例は、カタログ ファイルの署名にも、パブリックに利用可能なタイムスタンプ サーバーを使用します。 タイムスタンプ サーバーは VeriSign によって提供され、その URL が http://timestamp.verisign.com/scripts/timstamp.dllします。

```
SignTool sign /s TestCertificateStore /n AbcTestCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

### <a name="span-idverifyingexamplesspanspan-idverifyingexamplesspanverifying-examples"></a><span id="verifying_examples"></span><span id="VERIFYING_EXAMPLES"></span>例を確認しています

いることを確認する方法の例のシグネチャを次に、[ドライバー パッケージの](https://msdn.microsoft.com/library/windows/hardware/ff544840)カタログ ファイルがカーネル モード コード署名ポリシーと署名の要件、PnP デバイスのインストールに準拠します。 この例では、AbcCatalogFile.cat カタログ ファイルの署名を検証します。

```
SignTool verify /kp CatalogFileName.cat
```

次は、ドライバー パッケージのカタログ ファイルに示されたファイルの署名がカーネル モード コード署名ポリシーと署名の要件、PnP デバイスのインストールに準拠していることを確認する方法の例です。 この例では、AbcDriverPackage.inf、カタログ ファイル CatalogFileName.cat でサムプリントのエントリを持つ必要があるファイルの署名を検証します。

```
SignTool verify /kp /c CatalogFileName.cat AbcDriverPackage.inf
```

次は、埋め込みの署名がカーネル モードのコード署名では、Windows Vista および Windows の以降のバージョンのポリシーに準拠していることを確認する方法の例です。 この例では、AbcDriverFile.sys ドライバー ファイルに埋め込まれている署名を検証します。

```
SignTool verify /kp AbcDriverFile.sys
```

いることを確認する方法の例のシグネチャを次に、[ドライバー パッケージの](https://msdn.microsoft.com/library/windows/hardware/ff544840)カタログ ファイルは、PnP デバイス インストールの署名の要件に準拠します。 この例では、CatalogFileName.cat カタログ ファイルの署名を検証します。

```
SignTool verify /pa CatalogFileName.cat
```

### <a name="span-idexampleofaddingacatalogfiletothesystemcomponentdriverdataspanspan-idexampleofaddingacatalogfiletothesystemcomponentdriverdataspanexample-of-adding-a-catalog-file-to-the-system-component-driver-database"></a><span id="example_of_adding_a_catalog_file_to_the_system_component__driver__data"></span><span id="EXAMPLE_OF_ADDING_A_CATALOG_FILE_TO_THE_SYSTEM_COMPONENT__DRIVER__DATA"></span>カタログ ファイルをシステム コンポーネント (ドライバー) データベースに追加する例

SignTool を使用して、システム コンポーネント (ドライバー) データベースに CatalogFileName.cat カタログ ファイルを追加する方法の例は、次のです。 **/V**詳細モードで動作する SignTool を構成し、 **/u**オプションは、必要に応じて、置き換えられないようにする場合は、追加するには、カタログ ファイルの一意の名前を生成する SignTool を構成します、CatalogFileName.cat と同じ名前を持つカタログ ファイルが既に存在します。

```
SignTool catdb /v /u CatalogFileName.cat
```

 

 





