---
title: MakeCert
description: MakeCert (Makecert.exe) は、システム テストのルート キーによって、または別の指定したキーによって署名された X.509 証明書を作成するコマンド ライン CryptoAPI ツールです。
ms.assetid: 752aa806-5e8c-4519-bece-dcd91161b98a
keywords:
- MakeCert のドライバーの開発ツール
topic_type:
- apiref
api_name:
- MakeCert
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ded3ef7bebd2ba653e12b9c9efb5269fe4cde9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372754"
---
# <a name="makecert"></a>MakeCert


MakeCert (Makecert.exe) は、コマンド ライン[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)または別システム テストのルート キーによって署名された X.509 証明書を作成するツールは、キーを指定します。 証明書は、証明書の名前をキーのペアの公開部分にバインドします。 証明書は、ファイル、システムの証明書ストア、またはその両方に保存されます。

MakeCert は、スイッチの数が多いをサポートしていますが、このセクションでは、作成に関連する基本的なスイッチについてのみ説明、[テスト証明書](https://msdn.microsoft.com/library/windows/hardware/ff548693)テストへの署名を使用できる、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)を埋め込むか、ドライバー ファイルに署名します。

```
    MakeCert [/b DateStart] [/e DateEnd] [/len KeyLength] [/m nMonths] [/n "Name"] [/pe] [/r] [/sc SubjectCertFile] [/sk SubjectKey] [/sr SubjectCertStoreLocation] [/ss SubjectCertStoreName] [/sv SubjectKeyFile]OutputFile
```

### <a name="span-idpartiallistofswitchesandargumentsspanspan-idpartiallistofswitchesandargumentsspanpartial-list-of-switches-and-arguments"></a><span id="partial_list_of_switches_and_arguments"></span><span id="PARTIAL_LIST_OF_SWITCHES_AND_ARGUMENTS"></span>スイッチおよび引数の一覧の一部

<span id="_b_DateStart"></span><span id="_b_datestart"></span><span id="_B_DATESTART"></span>**/b** *DateStart*  
ときに、証明書が最初に有効な開始日を指定します。 形式*DateStart*年/月/日です。

場合、 **/b**スイッチが指定されていない、既定の開始日は、証明書が作成された日付。

<span id="_e_DateEnd"></span><span id="_e_dateend"></span><span id="_E_DATEEND"></span>**/e** *DateEnd*  
証明書の有効期間が終了する終了日を指定します。 形式*DateEnd*年/月/日です。

場合、 **/e**スイッチが指定されていない、既定の終了日が 12/31/2039 します。

<span id="_len_KeyLength"></span><span id="_len_keylength"></span><span id="_LEN_KEYLENGTH"></span>**/len** *KeyLength*  
サブジェクトのプライベートおよびパブリック キーのビット単位の長さを指定します。

/Len スイッチが指定されていない場合、既定のキー長は 1024 ビットが。

<span id="_m_nMonths"></span><span id="_m_nmonths"></span><span id="_M_NMONTHS"></span>**/m** *nMonths*  
証明書が有効には、開始日から開始する月の数を指定します。

<span id="_n__Name_"></span><span id="_n__name_"></span><span id="_N__NAME_"></span>**/n** "<em>Name</em>**"**  
証明書の名前を指定します。 この名前は、X.500 標準に準拠する必要があります。 最も簡単な方法は、使用する、"CN =*MyName*"形式です。

場合、 **/n**スイッチが指定されていない、証明書の既定の名前は「Joe のソフトウェアの店」。

<span id="_pe"></span><span id="_PE"></span>**/pe**  
MakeCert をエクスポート可能な証明書に関連付けられている秘密キーを構成します。

<span id="_r"></span><span id="_R"></span>**/r**  
MakeCert を自己署名ルート証明書を作成して構成します。

<span id="_sc_SubjectCertFile"></span><span id="_sc_subjectcertfile"></span><span id="_SC_SUBJECTCERTFILE"></span>**/sc** *SubjectCertFile*  
使用される既存のサブジェクト公開キーとサブジェクトの証明書ファイル名を指定します。

<span id="_sk_SubjectKey"></span><span id="_sk_subjectkey"></span><span id="_SK_SUBJECTKEY"></span>**/sk** *SubjectKey*  
秘密キーを保持する、サブジェクトのキー コンテナーの名前を指定します。 キー コンテナーが存在しない場合は、新しいキー コンテナーが作成されます。 どちらの場合 **/sk**も **/sv**スイッチに入ると、既定のキー コンテナーが作成され、既定で使用します。

<span id="_sr_SubjectCertStoreLocation"></span><span id="_sr_subjectcertstorelocation"></span><span id="_SR_SUBJECTCERTSTORELOCATION"></span>**/sr** *SubjectCertStoreLocation*  
証明書ストアのレジストリの場所を指定します。 *SubjectCertStoreLocation*引数は、次のいずれかである必要があります。

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
HKEY レジストリの場所を指定します\_現在\_ユーザー。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
HKEY レジストリの場所を指定します\_ローカル\_マシン。

場合、 **/r**と共にスイッチが指定されていない、 **/s**切り替えるには、 *currentUser*既定値です。

<span id="_ss_SubjectCertStoreName"></span><span id="_ss_subjectcertstorename"></span><span id="_SS_SUBJECTCERTSTORENAME"></span>**/ss** *SubjectCertStoreName*  
生成された証明書が保存されている証明書ストアの名前を指定します。

<span id="_sv_SubjectKeyFile"></span><span id="_sv_subjectkeyfile"></span><span id="_SV_SUBJECTKEYFILE"></span>**/sv** *SubjectKeyFile*  
秘密キーを保持する、サブジェクトの .pvk ファイルの名前を指定します。 どちらの場合 **/sk**も **/sv**スイッチに入ると、既定のキー コンテナーが作成され、既定で使用します。

<span id="OutputFile"></span><span id="outputfile"></span><span id="OUTPUTFILE"></span>*OutputFile*  
生成された証明書が保存されているファイルの名前。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

MakeCert は、スイッチの数が多いをサポートします。 このトピックで説明されているスイッチは、作成に使用できるものに制限されます、[テスト証明書](https://msdn.microsoft.com/library/windows/hardware/ff548693)します。

MakeCert のパラメーターの完全な一覧を参照してください、 [MakeCert](https://go.microsoft.com/fwlink/p/?linkid=62653) web サイト、および[MakeCert を使用して](https://go.microsoft.com/fwlink/p/?linkid=62655)web サイト。

MakeCert ツールの 32 ビット バージョンが、箱にある\\WDK の i386 フォルダー。 ツールの 64 ビット バージョンが、箱にある\\amd64 と bin\\WDK の ia64 フォルダー。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次の例では、MakeCert コマンドにという名前の"Contoso.com(Test)、"インストール テスト PrivateCertStore 証明書ストアに証明書し、テストのコピーを含む Testcert.cer ファイルを作成、テスト用の自己署名証明書が生成されます。証明書。

```
MakeCert -r -pe -ss PrivateCertStore -n "CN=Contoso.com(Test)" testcert.cer
```

 

 





