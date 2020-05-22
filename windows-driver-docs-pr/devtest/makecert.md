---
title: MakeCert
description: MakeCert (Makecert) は、システムテストルートキーまたは指定した別のキーによって署名された x.509 証明書を作成するコマンドライン CryptoAPI ツールです。
ms.assetid: 752aa806-5e8c-4519-bece-dcd91161b98a
keywords:
- MakeCert ドライバー開発ツール
topic_type:
- apiref
api_name:
- MakeCert
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c55b60f65a0b7a229948996fab045b7445b0d829
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769632"
---
# <a name="makecert"></a>MakeCert


MakeCert (Makecert) は、システムテストルートキーまたは指定した別のキーによって署名された x.509 証明書を作成するコマンドライン[CryptoAPI](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-portal)ツールです。 証明書は、キーペアの公開部分に証明書名をバインドします。 証明書は、ファイル、システム証明書ストア、またはその両方に保存されます。

MakeCert では多数のスイッチがサポートされていますが、このセクションでは、[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)のテスト署名またはドライバーファイルへの署名の埋め込みに使用できる[テスト証明書](https://docs.microsoft.com/windows-hardware/drivers/install/makecert-test-certificate)の作成に関連する基本的なスイッチについてのみ説明します。

```
    MakeCert [/b DateStart] [/e DateEnd] [/len KeyLength] [/m nMonths] [/n "Name"] [/pe] [/r] [/sc SubjectCertFile] [/sk SubjectKey] [/sr SubjectCertStoreLocation] [/ss SubjectCertStoreName] [/sv SubjectKeyFile]OutputFile
```

### <a name="span-idpartial_list_of_switches_and_argumentsspanspan-idpartial_list_of_switches_and_argumentsspanpartial-list-of-switches-and-arguments"></a><span id="partial_list_of_switches_and_arguments"></span><span id="PARTIAL_LIST_OF_SWITCHES_AND_ARGUMENTS"></span>スイッチと引数の部分的な一覧

<span id="_b_DateStart"></span><span id="_b_datestart"></span><span id="_B_DATESTART"></span>**/B** *datestart*  
証明書が最初に有効になる開始日を指定します。 *Datestart*の形式は mm/dd/yyyy です。

**/B**スイッチが指定されていない場合、既定の開始日は証明書が作成された日付になります。

<span id="_e_DateEnd"></span><span id="_e_dateend"></span><span id="_E_DATEEND"></span>**/E** *DateEnd*  
証明書の有効期間が終了する終了日を指定します。 *DateEnd*の形式は、mm/dd/yyyy です。

**/E**スイッチが指定されていない場合、既定の終了日は12/31/2039 です。

<span id="_len_KeyLength"></span><span id="_len_keylength"></span><span id="_LEN_KEYLENGTH"></span>**/len** *KeyLength*  
サブジェクトの秘密キーと公開キーの長さをビット単位で指定します。

/Len スイッチが指定されていない場合、既定のキーの長さは1024ビットになります。

<span id="_m_nMonths"></span><span id="_m_nmonths"></span><span id="_M_NMONTHS"></span>**/M** *nmonths*  
証明書が有効になる開始日からの月数を指定します。

<span id="_n__Name_"></span><span id="_n__name_"></span><span id="_N__NAME_"></span>**/n**"<em>Name</em>**"**  
証明書の名前を指定します。 この名前は X.500 標準に準拠する必要があります。 最も簡単な方法は、"CN =*MyName*" 形式を使用することです。

**/N**スイッチが指定されていない場合、証明書の既定の名前は "Joe'S Software Emporium" になります。

<span id="_pe"></span><span id="_PE"></span>**/pe**  
証明書に関連付けられている秘密キーをエクスポート可能にするように MakeCert を構成します。

<span id="_r"></span><span id="_R"></span>**r**  
自己署名ルート証明書を作成するように MakeCert を構成します。

<span id="_sc_SubjectCertFile"></span><span id="_sc_subjectcertfile"></span><span id="_SC_SUBJECTCERTFILE"></span>**/Sc** *subjectcertfile*  
サブジェクトの証明書のファイル名と、使用される既存のサブジェクトの公開キーを指定します。

<span id="_sk_SubjectKey"></span><span id="_sk_subjectkey"></span><span id="_SK_SUBJECTKEY"></span>**/sk** *subjectkey*  
秘密キーを保持するサブジェクトのキーコンテナーの名前を指定します。 キーコンテナーが存在しない場合は、新しいキーコンテナーが作成されます。 **または**、[]**スイッチが**入力されていない場合は、既定のキーコンテナーが作成され、既定で使用されます。

<span id="_sr_SubjectCertStoreLocation"></span><span id="_sr_subjectcertstorelocation"></span><span id="_SR_SUBJECTCERTSTORELOCATION"></span>**/sr** *SubjectCertStoreLocation*  
証明書ストアのレジストリの場所を指定します。 *SubjectCertStoreLocation*引数は、次のいずれかである必要があります。

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
レジストリの場所 HKEY CURRENT USER を指定し \_ \_ ます。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
レジストリの場所として HKEY ローカルコンピューターを指定し \_ \_ ます。

**/R**スイッチが **/s**スイッチと共に指定されていない場合、 *currentUser*が既定値になります。

<span id="_ss_SubjectCertStoreName"></span><span id="_ss_subjectcertstorename"></span><span id="_SS_SUBJECTCERTSTORENAME"></span>**/ss** *SubjectCertStoreName*  
生成された証明書を保存する証明書ストアの名前を指定します。

<span id="_sv_SubjectKeyFile"></span><span id="_sv_subjectkeyfile"></span><span id="_SV_SUBJECTKEYFILE"></span>**/sv**の*subjectkeyfile*  
秘密キーを保持するサブジェクトの .pvk ファイルの名前を指定します。 **または**、[]**スイッチが**入力されていない場合は、既定のキーコンテナーが作成され、既定で使用されます。

<span id="OutputFile"></span><span id="outputfile"></span><span id="OUTPUTFILE"></span>*OutputFile*  
生成された証明書が保存されるファイルの名前。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

MakeCert は多数のスイッチをサポートしています。 このトピックで説明するスイッチは、[テスト証明書](https://docs.microsoft.com/windows-hardware/drivers/install/makecert-test-certificate)の作成に使用できるスイッチに限定されています。

MakeCert パラメーターの完全な一覧については、 [MakeCert](https://docs.microsoft.com/windows/win32/seccrypto/makecert)の web サイトと「 [Using MakeCert](https://docs.microsoft.com/windows/win32/seccrypto/using-makecert) web サイト」を参照してください。

32ビット版の MakeCert ツールは、 \\ WDK の bin i386 フォルダーにあります。 64ビット版のツールは、 \\ WDK の bin amd64 および bin \\ ia64 フォルダーにあります。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次の例では、MakeCert コマンドによって "Contoso .com (Test)" という名前の自己署名テスト証明書が生成され、PrivateCertStore 証明書ストアにテスト証明書がインストールされ、テスト証明書のコピーを含む Testcert .cer ファイルが作成されます。

```
MakeCert -r -pe -ss PrivateCertStore -n "CN=Contoso.com(Test)" testcert.cer
```

 

 





