---
title: CertMgr
description: Certmgr.exe (Certmgr.exe) は、証明書、証明書信頼リスト (Ctl)、および証明書失効リスト (Crl) を管理するコマンドライン CryptoAPI ツールです。
ms.assetid: 860693f5-de64-4ca9-be64-23e2fbb862c5
keywords:
- Certmgr.exe ドライバー開発ツール
topic_type:
- apiref
api_name:
- CertMgr
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143d09773e7c52174a9426fab4114d05d1356065
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769646"
---
# <a name="certmgr"></a>CertMgr


Certmgr.exe (Certmgr.exe) は、証明書、証明書信頼リスト (Ctl)、および証明書失効リスト (Crl) を管理するコマンドライン[CryptoAPI](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-portal)ツールです。

Certmgr.exe では多数のスイッチがサポートされていますが、このセクションでは、証明書ストア内の[テスト証明書](https://docs.microsoft.com/windows-hardware/drivers/install/test-certificates)の管理に関連するものだけを説明します。

```
    CertMgr [/add|/del|/put] [Switches] [/s [/r RegistryLocation ] ] SourceName [/s [/r RegistryLocation] ] [DestinationName]
```

### <a name="span-idpartial_list_of_operations__switches__and_argumentsspanspan-idpartial_list_of_operations__switches__and_argumentsspanpartial-list-of-operations-switches-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、スイッチ、および引数の部分的な一覧

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>業務

<span id="add"></span><span id="ADD"></span>**アドイン**  
*SourceName*によって指定されたファイルから*destinationname*によって指定された証明書ストアに証明書、Ctl、または crl を追加するように certmgr.exe を構成します。

<span id="del"></span><span id="DEL"></span>**delete**  
*Destinationname*によって指定された証明書ストアから、 *SourceName*によって指定された証明書ストア内の証明書、Ctl、または crl を削除するように certmgr.exe を構成します。 *Destinationname*が指定されていない場合、 *SourceName*はコピー先ストアとしても機能し、変更されます。

<span id="put"></span><span id="PUT"></span>**投入**  
Certmgr.exe を構成して、 *SourceName*によって指定された証明書ストアの証明書、ctl、または Crl を*destinationname*で指定されたファイルに保存します。

<span id="none"></span><span id="NONE"></span>存在  
コマンドが指定されていない場合は、Certmgr.exe によって指定された証明書ストアまたはファイル内のすべての証明書、Ctl、または Crl が、 *SourceName*で表示されます。

### <a name="span-idswitches_and_argumentsspanspan-idswitches_and_argumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>スイッチと引数

<span id="_c"></span><span id="_C"></span>**スイッチ**  
*SourceName*によって指定されたファイルからの証明書のみを処理するように certmgr.exe を構成します。

<span id="_CTL"></span><span id="_ctl"></span>**/CTL**  
*SourceName*によって指定されたファイルからの ctl だけを処理するように certmgr.exe を構成します。

<span id="_CRL"></span><span id="_crl"></span>**/CRL**  
*SourceName*によって指定されたファイルからのみ crl を処理するように certmgr.exe を構成します。

<span id="_s"></span><span id="_S"></span>**/s**  
*SourceName*または*destinationname*によって指定された証明書ストアにシステムストアとしてアクセスするように certmgr.exe を構成します。

<span id="_r_registryLocation"></span><span id="_r_registrylocation"></span><span id="_R_REGISTRYLOCATION"></span>**/R** *registrylocation*  
システム証明書ストアのレジストリの場所を指定します。 **/R**スイッチは、 **/s**スイッチと共に使用する場合にのみ有効です。 *Registrylocation*引数は次のいずれかである必要があります。

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
レジストリの場所 HKEY CURRENT USER を指定し \_ \_ ます。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
レジストリの場所として HKEY ローカルコンピューターを指定し \_ \_ ます。

**/R**スイッチが **/s**スイッチと共に指定されていない場合、 *currentUser*が既定値になります。

これらの証明書ストアの詳細については、「[証明書ストア](https://docs.microsoft.com/windows-hardware/drivers/install/certificate-stores)」を参照してください。

<span id="_v"></span><span id="_V"></span>**/v**  
証明書、Ctl、および Crl に関する詳細情報を表示するように Certmgr.exe を構成します。 このスイッチが指定されていない場合、Certmgr.exe には簡単な情報のみが表示されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

Certmgr.exe を使用するには、ユーザーがシステムの Administrators グループのメンバーであり、管理者特権でのコマンドプロンプトからコマンドを実行する必要があります。

Certmgr.exe パラメーターの完全な一覧については、[証明書マネージャーツール](https://docs.microsoft.com/dotnet/framework/tools/certmgr-exe-certificate-manager-tool)の web サイトを参照してください。

32ビット版の Certmgr.exe ツールは、WDK の*bin \\ i386*フォルダーにあります。 64ビット版のツールは、 \\ WDK の bin amd64 および bin \\ ia64 フォルダーにあります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の2つの Certmgr.exe コマンドは、 *OutputFile*ファイルの証明書を、信頼されたルート証明機関の証明書ストアおよび信頼された発行元の証明書ストアに追加します。

```
CertMgr /add OutputFile.cer /s /r localMachine root 
CertMgr /add OutputFile.cer /s /r localMachine trustedpublisher
```

 

 





