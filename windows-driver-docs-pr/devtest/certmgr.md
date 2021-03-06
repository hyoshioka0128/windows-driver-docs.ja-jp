---
title: CertMgr
description: CertMgr (Certmgr.exe) は、証明書を管理するコマンド ライン CryptoAPI ツール、証明書信頼リスト (Ctl)、および証明書失効リスト (Crl)。
ms.assetid: 860693f5-de64-4ca9-be64-23e2fbb862c5
keywords:
- CertMgr ドライバー開発ツール
topic_type:
- apiref
api_name:
- CertMgr
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e68db909d8b8f99f148e179dd9bcda1417230247
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371616"
---
# <a name="certmgr"></a>CertMgr


CertMgr (Certmgr.exe) は、コマンド ライン[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)証明書、証明書信頼リスト (Ctl)、および証明書失効リスト (Crl) を管理するツール。

CertMgr は、スイッチの数が多いをサポートしますが、このセクションでは、管理に関連するもののみについて説明します[テスト証明書](https://docs.microsoft.com/windows-hardware/drivers/install/test-certificates)証明書ストア内で。

```
    CertMgr [/add|/del|/put] [Switches] [/s [/r RegistryLocation ] ] SourceName [/s [/r RegistryLocation] ] [DestinationName]
```

### <a name="span-idpartiallistofoperationsswitchesandargumentsspanspan-idpartiallistofoperationsswitchesandargumentsspanpartial-list-of-operations-switches-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、スイッチ、および引数の一覧の一部

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>操作

<span id="add"></span><span id="ADD"></span>**追加します。**  
構成で指定されたファイルから証明書、Ctl、または Crl を追加する CertMgr *SourceName*で指定された証明書ストアに*DestinationName*します。

<span id="del"></span><span id="DEL"></span>**Del**  
構成証明書、Ctl、または Crl で指定された証明書ストアを削除する CertMgr *SourceName*で指定された証明書ストアから*DestinationName*します。 場合*DestinationName*が指定されていない*SourceName*保存先ストアとしても機能し、変更されます。

<span id="put"></span><span id="PUT"></span>**配置**  
CertMgr の証明書、Ctl、または Crl で指定された証明書ストアからの保存を構成します。 *SourceName*によって指定されたファイルに*DestinationName*します。

<span id="none"></span><span id="NONE"></span>[なし]  
CertMgr が証明書ストアまたはで指定されたファイルで、すべての証明書、Ctl、または Crl を表示するコマンドが指定されていない場合*SourceName*します。

### <a name="span-idswitchesandargumentsspanspan-idswitchesandargumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>スイッチと引数

<span id="_c"></span><span id="_C"></span> **/c**  
構成のみで指定されたファイルから証明書を処理する CertMgr *SourceName*します。

<span id="_CTL"></span><span id="_ctl"></span> **/CTL**  
構成のみで指定されたファイルから Ctl を処理する CertMgr *SourceName*します。

<span id="_CRL"></span><span id="_crl"></span> **/CRL**  
構成のみで指定されたファイルからの Crl を処理する CertMgr *SourceName*します。

<span id="_s"></span><span id="_S"></span> **/s**  
構成で指定された証明書ストアにアクセスする CertMgr *SourceName*または*DestinationName*システム ストアとして。

<span id="_r_registryLocation"></span><span id="_r_registrylocation"></span><span id="_R_REGISTRYLOCATION"></span> **/r** *registryLocation*  
システムの証明書ストアのレジストリの場所を指定します。 **/R**スイッチが有効なで使用する場合のみ、 **/s**スイッチします。 *RegistryLocation*引数はいずれかである必要があります。

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
HKEY レジストリの場所を指定します\_現在\_ユーザー。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
HKEY レジストリの場所を指定します\_ローカル\_マシン。

場合、 **/r**と共にスイッチが指定されていない、 **/s**切り替えるには、 *currentUser*既定値です。

これらの証明書ストアの詳細については、次を参照してください。[証明書ストア](https://docs.microsoft.com/windows-hardware/drivers/install/certificate-stores)します。

<span id="_v"></span><span id="_V"></span> **/v**  
CertMgr の証明書、Ctl、および Crl に関する詳細情報を表示するよう構成します。 このスイッチが指定されていない場合、CertMgr には簡単な情報のみが表示されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

CertMgr を使用するには、ユーザーは、システムの Administrators グループのメンバーであるし、管理者特権のコマンド プロンプトからコマンドを実行する必要があります。

CertMgr パラメーターの完全な一覧を参照してください、[証明書マネージャー ツール](https://go.microsoft.com/fwlink/p/?linkid=70233)web サイト。

CertMgr ツールの 32 ビット バージョンがあります、 *bin\\i386* WDK のフォルダー。 ツールの 64 ビット バージョンが、箱にある\\amd64 と bin\\WDK の ia64 フォルダー。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の 2 つの CertMgr コマンド ファイル内の証明書の追加*OutputFile.cer*に信頼されたルート証明機関ストアと信頼された発行元証明書ストアの証明書します。

```
CertMgr /add OutputFile.cer /s /r localMachine root 
CertMgr /add OutputFile.cer /s /r localMachine trustedpublisher
```

 

 





