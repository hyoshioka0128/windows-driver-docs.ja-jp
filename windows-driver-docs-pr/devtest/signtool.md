---
title: SignTool
description: SignTool (Signtool) は、ファイルのデジタル署名、ファイルの署名の検証、およびタイムスタンプファイルを行うコマンドライン CryptoAPI ツールです。
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
ms.openlocfilehash: baef109a7cd61805247c469596adb258804effc1
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063946"
---
# <a name="signtool"></a>SignTool


SignTool (Signtool) は、ファイルのデジタル署名、ファイルの署名の検証、およびタイムスタンプファイルを行うコマンドライン[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)ツールです。

```
    SignTool [Operation] [Options] [FileName ...]
```

### <a name="span-idpartial_list_of_operations__switches__and_argumentsspanspan-idpartial_list_of_operations__switches__and_argumentsspanpartial-list-of-operations-options-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、オプション、および引数の部分的な一覧

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>業務

<span id="catdb"></span><span id="CATDB"></span>**catdb**  
カタログデータベースを更新するように SignTool を構成します。 SignTool は、カタログファイルをデータベースに追加するか、データベースからカタログを削除します。 既定では、 **catdb**コマンドは、 *FileName*引数で指定された名前を持つファイルをシステムコンポーネント (ドライバー) データベースに追加します。

**注カタログデータベース**は、カタログファイルの自動検索に使用されます。  

 

<span id="sign"></span><span id="SIGN"></span>**シャープ**  
*FileName*引数で指定された名前を持つファイルをデジタル署名するように SignTool を構成します。

<span id="timestamp"></span><span id="TIMESTAMP"></span>**タイムスタンプ**  
*FileName*引数で指定された名前を持つファイルにタイムスタンプを設定するように SignTool を構成します。

<span id="verify"></span><span id="VERIFY"></span>**か**  
*FileName*引数によって名前が指定されているファイルのデジタル署名を確認するように SignTool を構成します。

### <a name="span-idcatdb_operation_switchesspanspan-idcatdb_operation_switchesspancatdb-operation-options"></a><span id="catdb_operation_switches"></span><span id="CATDB_OPERATION_SWITCHES"></span>Catdb 操作オプション

<span id="_d"></span><span id="_D"></span>**d**  
カタログデータベースを更新するように SignTool を構成します。 **/D**も **/g**オプションも使用しない場合、SignTool はシステムコンポーネントとドライバーデータベースを更新します。

<span id="_g_Guid"></span><span id="_g_guid"></span><span id="_G_GUID"></span> **/g** *Guid*  
*GUID*引数によって識別されるカタログデータベースを更新するように SignTool を構成します。

<span id="_r"></span><span id="_R"></span>**r**  
SignTool を構成して、名前が*FileName*引数で指定されている各カタログファイルをカタログデータベースから削除します。 このオプションを指定しない場合、SignTool は指定されたカタログファイルをカタログデータベースに追加します。

<span id="_u"></span><span id="_U"></span> **/u**  
必要に応じて、カタログファイルに対して一意の名前を生成するように SignTool を構成して、カタログデータベース内の既存のカタログファイルと競合しないようにします。 このオプションが指定されていない場合、SignTool は、追加するカタログと同じ名前を持つ既存のカタログを上書きします。

### <a name="span-idsign_operation_switchesspanspan-idsign_operation_switchesspansign-operation-options"></a><span id="sign_operation_switches"></span><span id="SIGN_OPERATION_SWITCHES"></span>Sign 操作オプション

<span id="_a_"></span><span id="_A_"></span> **/a**    
最適な署名証明書を自動的に選択するように SignTool を構成します。 このオプションが指定されていない場合、SignTool は、署名証明書を1つだけ検索することを想定しています。

<span id="_ac_CrossCertFileName"></span><span id="_ac_crosscertfilename"></span><span id="_AC_CROSSCERTFILENAME"></span> **/ac** *クロス Certfilename*  
" *StoreName*" という名前のソフトウェア発行元証明書 (SPC) で使用され、証明書ストアにインストールされるクロス証明書ファイルの名前を指定します。 このオプションは、署名証明書が SPC の場合にのみ使用してください。

<span id="_c_CertTemplateName"></span><span id="_c_certtemplatename"></span><span id="_C_CERTTEMPLATENAME"></span> **/c** *Certtemplatename*  
署名証明書の証明書テンプレート名 (Microsoft 拡張機能) を指定します。

<span id="_csp_CSPName"></span><span id="_csp_cspname"></span><span id="_CSP_CSPNAME"></span> **/csp** *Cspname*  
秘密キーコンテナーを含む暗号化サービスプロバイダー (CSP) を指定します。

<span id="_d_Desc"></span><span id="_d_desc"></span><span id="_D_DESC"></span> **/d** *Desc*  
署名されたコンテンツの説明を指定します。

<span id="_du_URL"></span><span id="_du_url"></span><span id="_DU_URL"></span> **/du** *URL*  
署名されたコンテンツの展開された説明の URL を指定します。

<span id="_f_SignCertFile"></span><span id="_f_signcertfile"></span><span id="_F_SIGNCERTFILE"></span> **/f** *Signcertfile*  
ファイル内の署名証明書を指定します。 Personal Information Exchange (PFX) ファイル形式のみがサポートされています。 [**Pvk2Pfx**](pvk2pfx.md)ツールを使用すると、SPC ファイルと .pvk ファイルを PFX 形式に変換できます。

ファイルがパスワードで保護された PFX 形式の場合は、 **/p**オプションを使用してパスワードを指定します。 ファイルに秘密キーが含まれていない場合は、 **/csp**オプションと **/k**オプションを使用して、csp と秘密キーコンテナー名をそれぞれ指定します。

<span id="_fd"></span><span id="_FD"></span> **/fd**  
ファイルの署名を作成する際に使うファイル ダイジェスト アルゴリズムを指定します。 既定値は SHA1 です。

<span id="_i_IssuerName"></span><span id="_i_issuername"></span><span id="_I_ISSUERNAME"></span> **/i**発行する  
署名証明書の発行者の名前を指定します。 この値には、発行者名全体の部分文字列を指定できます。

<span id="_j_DLL"></span><span id="_j_dll"></span><span id="_J_DLL"></span> **/j** *DLL*  
署名の属性を提供する DLL の名前を指定します。

<span id="_jp_ParameterName"></span><span id="_jp_parametername"></span><span id="_JP_PARAMETERNAME"></span> **/jp** *ParameterName*  
**/J**コマンドによって指定された DLL に渡されるパラメーターを指定します。

<span id="_kc_PrivKeyContainerName"></span><span id="_kc_privkeycontainername"></span><span id="_KC_PRIVKEYCONTAINERNAME"></span> **/kc** *Privkeycontainername*  
秘密キーのキーコンテナー名を指定します。

<span id="_n_SubjectName"></span><span id="_n_subjectname"></span><span id="_N_SUBJECTNAME"></span> **/n** *SubjectName*  
署名証明書のサブジェクトの名前を指定します。 この値は、サブジェクト名の一部でもかまいません。

<span id="_nph"></span><span id="_NPH"></span> **/nph**  
サポートされている場合、実行可能ファイルのページハッシュを抑制します。 既定値は、SIGNTOOL\_PAGE\_ハッシュ環境変数および wintrust .dll バージョンによって決まります。 このオプションは、非 PE ファイルでは無視されます。

<span id="_p_Password"></span><span id="_p_password"></span><span id="_P_PASSWORD"></span> **/p** *パスワード*  
PFX ファイルを開く時に使うパスワードを指定します PFX ファイルは、 **/f**オプションを使用して指定できます。

<span id="_p7__Path"></span><span id="_p7__path"></span><span id="_P7__PATH"></span> **/p7** *パス*  
指定された各コンテンツファイルに対して\#公開キー暗号化標準 (PKCS) 7 ファイルが生成されることを指定します。 PKCS \#7 ファイルはパス\\filename. p7 という名前です。

<span id="_p7ce_Value"></span><span id="_p7ce_value"></span><span id="_P7CE_VALUE"></span> **/p7ce** *値*  
署名された PKCS \#7 コンテンツのオプションを指定します。 署名されたコンテンツを pkcs \#7 ファイルに埋め込む場合は Value を "Embedded" に設定し、デタッチされた pkcs \#7 ファイルの署名されたデータ部分を生成する場合は "DetachedSignedData" に設定します。 **/P7ce**オプションが使用されていない場合は、署名されたコンテンツが既定で埋め込まれます。

<span id="_p7co__OID"></span><span id="_p7co__oid"></span><span id="_P7CO__OID"></span> **/p7co** *OID*  
署名された PKCS \#7 コンテンツを識別するオブジェクト識別子 (OID) を指定します。

<span id="_ph___"></span><span id="_PH___"></span> **/ph 前処理時**    
サポートされている場合、実行可能ファイルのページハッシュを生成します。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span> **/r** *RootSubjectName*  
署名証明書をチェーンする必要のあるルート証明書のサブジェクト名を指定します。 この値には、ルート証明書のサブジェクト名全体の部分文字列を指定できます。

<span id="_s_StoreName"></span><span id="_s_storename"></span><span id="_S_STORENAME"></span> **/s** *StoreName*  
ファイルの署名に使用する証明書を検索するときに開く証明書ストアの名前を指定します。 このオプションが指定されていない場合、 **My**証明書ストアが開きます。

<span id="_sha1_Hash"></span><span id="_sha1_hash"></span><span id="_SHA1_HASH"></span> **/sha1** *ハッシュ*  
署名証明書の SHA1 ハッシュを指定します。

<span id="_sm"></span><span id="_SM"></span> **/sm**  
ユーザー証明書ストアではなく、コンピューターの証明書ストアを使用するように SignTool を構成します。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span> **/t** *URL*  
タイムスタンプサーバーの URL を指定します。 このオプションが指定されていない場合、署名されたファイルはタイムスタンプを持ちません。 カタログファイルまたはドライバーファイルはタイムスタンプにする必要があります。これは、署名者のキーが侵害された場合に、ファイルの署名に使用されたキーを失効させるために必要な情報がタイムスタンプによって提供されるためです。

<span id="_td____alg"></span><span id="_TD____ALG"></span> **/td** *alg*  
RFC 3161 タイムスタンプサーバーで使用されるダイジェストアルゴリズムを要求するために、/tr オプションと共に使用されます。

<span id="_tr___URL"></span><span id="_tr___url"></span><span id="_TR___URL"></span> **/tr** *URL*  
RFC 3161 タイムスタンプサーバーの URL を指定します。 このオプション (または **/t**) が存在しない場合、署名されたファイルにはタイムスタンプが付きません。 タイムスタンプが失敗した場合は、警告が生成されます。 このオプションは、 **/t**オプションと共に使用することはできません。

<span id="_u___Usage"></span><span id="_u___usage"></span><span id="_U___USAGE"></span> **/u** *使用法*  
署名証明書に存在する必要がある拡張キー使用法 (EKU) を指定します。 使用状況の値は、OID または文字列によって指定できます。 既定の使用法は "コード署名" (1.3.6.1.5.5.7.3.3) です。

<span id="_uw_"></span><span id="_UW_"></span> **/uw**    
"Windows システムコンポーネントの検証" (1.3.6.1.4.1.311.10.3.6) の使用法を指定します。

### <a name="span-idtimestamp_operation_switchesspanspan-idtimestamp_operation_switchesspantimestamp-operation-options"></a><span id="timestamp_operation_switches"></span><span id="TIMESTAMP_OPERATION_SWITCHES"></span>タイムスタンプ操作のオプション

<span id="_p7_"></span><span id="_P7_"></span> **/p7**    
PKCS \#7 ファイルにタイムスタンプをします。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span> **/t** *URL*  
タイムスタンプサーバーの URL を指定します。 タイムスタンプが設定されているファイルは、以前に署名されている必要があります

<span id="_td___alg"></span><span id="_TD___ALG"></span> **/td** *alg*  
RFC 3161 タイムスタンプサーバーで使用されるダイジェストアルゴリズムを要求します。 **/td**は、 **/tr**オプションと共に使用されます。

<span id="_tp__index"></span><span id="_TP__INDEX"></span> **/tp** *インデックス*  
インデックスで署名にタイムスタンプを付けます。

<span id="_tr___alg"></span><span id="_TR___ALG"></span> **/tr** *alg*  
RFC 3161 タイムスタンプサーバーで使用されるダイジェストアルゴリズムを要求します。 **/td**は、 **/tr**オプションと共に使用されます。

### <a name="span-idverify_operation_switchesspanspan-idverify_operation_switchesspanverify-operation-options"></a><span id="verify_operation_switches"></span><span id="VERIFY_OPERATION_SWITCHES"></span>操作オプションの確認

<span id="_a"></span><span id="_A"></span> **/a**  
ファイルの検証にすべてのメソッドを使用できることを指定します。 まず、カタログデータベースを検索して、カタログでファイルが署名されているかどうかを確認します。 ファイルがどのカタログにも署名されていない場合、SignTool はファイルの埋め込み署名を検証しようとします。 このオプションは、カタログで署名されている可能性があるファイルまたは署名されていないファイルを検証する場合に推奨されます。

<span id="_ad"></span><span id="_AD"></span> **/ad**  
ファイルがサインインしているカタログの既定のカタログデータベースのみを検索するように指定します。

<span id="_all"></span><span id="_ALL"></span> **/all**  
複数の署名を含むファイル内のすべての署名を検証します。

<span id="_as"></span><span id="_AS"></span> **/as**  
ファイルがサインインしているカタログを検索するシステムコンポーネント (ドライバー) カタログデータベースのみを指定します。

<span id="_ag_CatDBGUID"></span><span id="_ag_catdbguid"></span><span id="_AG_CATDBGUID"></span>**ag***Catdbguid*  
ファイルがサインインされたカタログを検索するために、 *Catdbguid*引数で識別されるカタログデータベースのみを指定します。

<span id="_c___CatalogFileName"></span><span id="_c___catalogfilename"></span><span id="_C___CATALOGFILENAME"></span> **/c** *Catalogfilename*  
カタログファイルの名前を指定します。

<span id="_d___"></span><span id="_D___"></span>**d**   
署名ツールで説明と説明の URL を出力するように指定します。

<span id="_ds___index"></span><span id="_DS___INDEX"></span> **/ds** *インデックス*  
指定した位置にある署名を検証します。

<span id="_hash__SHA1SHA256"></span><span id="_hash__sha1sha256"></span><span id="_HASH__SHA1SHA256"></span> **/ハッシュ**{**SHA1**|**SHA256**}  
カタログ内のファイルを検索するときに使用するオプションのハッシュアルゴリズムを指定します。

<span id="_kp"></span><span id="_KP"></span> **/kp**  
*FileName*引数で指定された各ファイルのデジタル署名が、[カーネルモードコード署名ポリシー](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)および Windows Vista の[PnP デバイスインストール署名要件](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)に準拠していることを確認するように SignTool を構成します。およびそれ以降のバージョンの Windows。 このオプションが指定されていない場合、SignTool は、署名が PnP デバイスのインストール署名要件に準拠しているかどうかのみを確認します。

<span id="_ms"></span><span id="_MS"></span> **/ミリ秒**  
複数の検証セマンティクスを使用します。 これは、Windows 8 以降での[**WinVerifyTrust 関数**](https://docs.microsoft.com/windows/desktop/api/wintrust/nf-wintrust-winverifytrust)呼び出しの既定の動作です。

<span id="_o_Version"></span><span id="_o_version"></span><span id="_O_VERSION"></span> **/o** *バージョン*  
オペレーティングシステムのバージョンに従ってファイルを検証します。 *バージョン*引数の形式は<em>platformid</em> **:** <em>vermajor</em>**です。** <em>Verminor</em> **.** このように

**/O**オプションを使用することをお勧めします。 **/O**が指定されていない場合、SignTool は予期しない結果を返す可能性があります。 たとえば、 **/o**オプションを指定しない場合、古いオペレーティングシステム上で正しく検証されるシステムカタログが、新しいオペレーティングシステムで正しく検証されない可能性があります。

<span id="_p7"></span><span id="_P7"></span> **/p7**  
PKCS \#7 ファイルを検証します。 既存のポリシーは、PKCS \#7 の検証には使用されません。 署名がチェックされ、署名証明書のチェーンが作成されます。

<span id="_pa"></span><span id="_PA"></span> **/pa**  
*FileName*引数で指定された各ファイルのデジタル署名が[PnP デバイスのインストール署名要件](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)に準拠していることを確認するように SignTool を構成します。

**メモこのオプション**は、catdb オプションと共に使用することはできません。   

 

<span id="_pg__PolicyGUID"></span><span id="_pg__policyguid"></span><span id="_PG__POLICYGUID"></span> **/pg** *Policyguid*  
GUID によって検証ポリシーを指定します。 PolicyGUID は、検証ポリシーの ActionID に対応しています。

**メモこのオプション**は、catdb オプションと共に使用することはできません。   

 

<span id="_ph__"></span><span id="_PH__"></span> **/ph 前処理時**    
署名ツールでページハッシュ値を出力および確認する必要があることを指定します。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span> **/r** *RootSubjectName*  
署名証明書をチェーンする必要のあるルート証明書のサブジェクト名を指定します。 この値には、ルート証明書のサブジェクト名全体の部分文字列を指定できます。

<span id="_tw"></span><span id="_TW"></span> **/tw**  
署名にタイムスタンプがない場合に警告を生成することを指定します。

### <a name="span-idgeneral_switchesspanspan-idgeneral_switchesspangeneral-options"></a><span id="general_switches"></span><span id="GENERAL_SWITCHES"></span>全般オプション

<span id="_q"></span><span id="_Q"></span> **/q**  
実行が成功した場合に出力しないように SignTool を構成し、実行に失敗した場合は最小限の出力を表示します。

<span id="_v"></span><span id="_V"></span> **/v**  
操作と警告メッセージの詳細バージョンを表示するように SignTool を構成します。

<span id="__"></span> **/?**  
ヘルプ情報をコマンドウィンドウに表示するように SignTool を構成します。

<span id="FileName_..."></span><span id="filename_..."></span><span id="FILENAME_..."></span>*ファイル名...*  
1つ以上のファイル名のリストを指定します。 SignTool は、コマンドに応じて、指定されたファイルの署名、タイムスタンプ、または確認を行います。 **Catdb**コマンドが使用されている場合、SignTool は、カタログデータベースから指定されたファイルを追加または削除します。

**Sign**、 **timestamp**、および**verify**コマンドの場合、ファイルは[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)またはドライバーファイルのカタログファイルにすることができます。

**Catdb**コマンドの場合、ファイルは[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)のカタログファイルである必要があります。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

SignTool は多数のオプションをサポートしています。 このトピックで説明するオプションは、ドライバーパッケージまたはドライバーファイルの署名または検証に使用できるものに限定されています。

SignTool パラメーターの完全な一覧については、Microsoft [SignTool](https://go.microsoft.com/fwlink/p/?linkid=62661)の web サイトを参照してください。

ファイルの署名の詳細については、Microsoft[暗号化ツール](https://go.microsoft.com/fwlink/p/?linkid=10637)の web サイトを参照してください。

32ビットバージョンの SignTool は、WDK の bin\\i386 フォルダーにあります。 64ビット版のツールは、WDK の bin\\amd64 および bin\\ia64 フォルダーにあります。

### <a name="span-idsigning_examplesspanspan-idsigning_examplesspansigning-examples"></a><span id="signing_examples"></span><span id="SIGNING_EXAMPLES"></span>署名の例

ソフトウェア発行元証明書 (SPC) と対応するクロス証明書を使用して、[ドライバーパッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)カタログファイルに署名する方法の例を次に示します。 この例は、カーネルモードのコード署名ポリシーを適用する Windows Vista 以降のバージョンの windows で、ドライバー64パッケージに署名する場合に有効です。 この例では、ドライバーパッケージのカタログファイル AbcCatFileName.cat に署名します。 カタログファイルに署名するために、この例では、クロス証明書の AbcCrossCertificate と AbcSPCCertificate 証明書を使用します。 AbcSPCCertificate 証明書は、AbcCertificateStore 証明書ストアにあります。

また、この例では、一般公開されているタイムスタンプサーバーを使用してカタログファイルに署名します。 タイムスタンプサーバーは DigiCert によって提供され http://timestamp.digicert.com 、その URL はです。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcCatFileName.cat
```

次に、SPC とクロス証明書を使用して、ドライバーファイルに署名を埋め込む方法の例を示します。 すべてのパラメーターは、カタログファイルに署名する例と同じです。ただし、署名されたファイルは、カタログファイル AbcCatFileName.cat ではなく AbcDriverFile です。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcDriverFile.sys
```

[商用リリース証明](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-release-certificate)書または[商用テスト証明書](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-test-certificate)を使用して、[ドライバーパッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)カタログファイルに署名する方法の例を次に示します。 この例は、カーネルモードのコード署名ポリシーを適用しない windows Vista 以降のバージョンの windows で、ドライバー32パッケージに署名する場合に有効です。 この例では、ドライバーパッケージのカタログファイル CatalogFileName.cat に署名します。 この例では、TestCertificateStore 証明書ストアにある AbcTestCertificate テスト証明書を使用して、カタログファイルに署名します。

また、この例では、一般公開されているタイムスタンプサーバーを使用してカタログファイルに署名します。 タイムスタンプサーバーは DigiCert によって提供され http://timestamp.digicert.com 、その URL はです。

```
SignTool sign /s TestCertificateStore /n AbcTestCertificate /t http://timestamp.digicert.com CatalogFileName.cat
```

### <a name="span-idverifying_examplesspanspan-idverifying_examplesspanverifying-examples"></a><span id="verifying_examples"></span><span id="VERIFYING_EXAMPLES"></span>検証 (例を)

次に示すのは、[ドライバーパッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)カタログファイルの署名が、カーネルモードのコード署名ポリシーと PnP デバイスのインストール署名要件に準拠しているかどうかを確認する方法の例です。 この例では、カタログファイル AbcCatalogFile.cat の署名を確認します。

```
SignTool verify /kp CatalogFileName.cat
```

次に、ドライバーパッケージのカタログファイルに一覧表示されているファイルの署名が、カーネルモードのコード署名ポリシーと PnP デバイスのインストール署名要件に準拠しているかどうかを確認する方法の例を示します。 この例では、AbcDriverPackage ファイルの署名を確認します。この署名には、カタログファイル CatalogFileName.cat に拇印エントリが必要です。

```
SignTool verify /kp /c CatalogFileName.cat AbcDriverPackage.inf
```

埋め込まれた署名が Windows Vista 以降のバージョンの Windows でカーネルモードコード署名ポリシーに準拠しているかどうかを確認する方法の例を次に示します。 この例では、ドライバーファイル AbcDriverFile に埋め込まれている署名を確認します。

```
SignTool verify /kp AbcDriverFile.sys
```

[ドライバーパッケージの](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)カタログファイルの署名が PnP デバイスのインストール署名要件に準拠しているかどうかを確認する方法の例を次に示します。 この例では、カタログファイル CatalogFileName.cat の署名を確認します。

```
SignTool verify /pa CatalogFileName.cat
```

### <a name="span-idexample_of_adding_a_catalog_file_to_the_system_component__driver__dataspanspan-idexample_of_adding_a_catalog_file_to_the_system_component__driver__dataspanexample-of-adding-a-catalog-file-to-the-system-component-driver-database"></a><span id="example_of_adding_a_catalog_file_to_the_system_component__driver__data"></span><span id="EXAMPLE_OF_ADDING_A_CATALOG_FILE_TO_THE_SYSTEM_COMPONENT__DRIVER__DATA"></span>カタログファイルをシステムコンポーネント (ドライバー) データベースに追加する例

SignTool を使用してカタログファイル CatalogFileName.cat をシステムコンポーネント (ドライバー) データベースに追加する方法の例を次に示します。 **/V**オプションを指定すると、SignTool は詳細モードで動作するように構成されます。 **/u**オプションでは、必要に応じて、追加するカタログファイルの一意の名前を生成するように SignTool を構成します。これにより、同じ既存のカタログファイルが置き換えられるのを防ぐことができます。名前を CatalogFileName.cat とします。

```
SignTool catdb /v /u CatalogFileName.cat
```

 

 





