---
title: USB 記憶装置用の証明書の作成
description: 記憶域証明書の管理の強化されたツールは、IEEE 1667 準拠 USB 記憶装置にインポートされている自己署名証明書を作成できます。
ms.assetid: c63e69c3-ba60-417e-8838-825d81ac7301
keywords:
- USB ストレージ デバイス ドライバーの開発ツールの証明書の作成
topic_type:
- apiref
api_name:
- Creating
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9fcf3fc5d6ce2bc40e5866c763a8913f5db3dca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380968"
---
# <a name="creating-certificates-for-usb-storage-devices"></a>USB 記憶装置用の証明書の作成


記憶域証明書の管理の強化されたツールは、IEEE 1667 準拠 USB 記憶装置にインポートされている自己署名証明書を作成できます。 証明書の仕様では、テキスト (.txt)、または初期化 (.ini) ファイル内に格納され、次のエントリを含める必要があります。

```
  [certificate]

    Subject=SubjectString
SignatureAlgorithm=[RSASSA-PSS-SHA1|
        RSASSA-PSS-SHA384|
        RSASSA-PSS-SHA512|
        RSASSA-PKCS1_5-SHA1|
        RSASSA-PKCS1_5-SHA256|
        RSASSA-PKCS1_5-SHA384|
        RSASSA-PKCS1_5-SHA512]
KeyType=RSAKeyStrength=[1024|2048|3072]
ExpirationDate=mm/dd/yy
[SelfSigned=[YES|NO]]
[OrganizationName=OrgNameString]
[OrganizationUnit=OrgUnitString]
[CompanyLocation=LocationString]
[State=StateString]
[ZipCode=ZipCodeString]
[Country=CountryString]
```

## <a name="span-identriesspanspan-identriesspanspan-identriesspanentries"></a><span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>エントリ


<span id="_______Subject______"></span><span id="_______subject______"></span><span id="_______SUBJECT______"></span> **件名**   
これに必要なエントリは、サブジェクトの証明書の名前を指定します。 この名前は、X.509 標準に準拠する必要があります。

<span id="_______SignatureAlgorithm______"></span><span id="_______signaturealgorithm______"></span><span id="_______SIGNATUREALGORITHM______"></span> **SignatureAlgorithm**   
これに必要なエントリは、デジタル証明書の署名に使用されるアルゴリズムを指定します。 署名アルゴリズムは、次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SignatureAlgorithm 値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PSS-SHA1</strong></p></td>
<td align="left"><p>160 ビット sha-1 ハッシュ アルゴリズムを使用して、RSASSA-PSS デジタル署名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PSS-SHA256</strong></p></td>
<td align="left"><p>256 ビットの sha-256 ハッシュ アルゴリズムを使用して、RSASSA-PSS デジタル署名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PSS-SHA384</strong></p></td>
<td align="left"><p>384 ビット sha-384 ハッシュ アルゴリズムを使用して RSASSA-PSS デジタル署名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PSS-SHA512</strong></p></td>
<td align="left"><p>512 ビットの sha-512 ハッシュ アルゴリズムを使用して RSASSA-PSS デジタル署名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA1</strong></p></td>
<td align="left"><p>160 ビット sha-1 ハッシュ アルゴリズムを使用して、RSASSA PKCS1_5 (PKCS #1 バージョン 1.5) デジタル署名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA256</strong></p></td>
<td align="left"><p>256 ビットの sha-256 ハッシュ アルゴリズムを使用して、RSASSA PKCS1_5 デジタル署名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA384</strong></p></td>
<td align="left"><p>384 ビット sha-384 ハッシュ アルゴリズムを使用して RSASSA PKCS1_5 デジタル署名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA512</strong></p></td>
<td align="left"><p>512 ビットの sha-512 ハッシュ アルゴリズムを使用して RSASSA PKCS1_5 デジタル署名。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______KeyType______"></span><span id="_______keytype______"></span><span id="_______KEYTYPE______"></span> **KeyType**   
この必要なエントリは、サブジェクトのキーの種類を指定します。 Windows 7 以降、このエントリの値をいる必要があります**RSA**します。

<span id="_______KeyStrengh______"></span><span id="_______keystrengh______"></span><span id="_______KEYSTRENGH______"></span> **KeyStrengh**   
これは、必須の長さ (ビット単位) に基づくと、キーの強度を指定します。

<span id="_______SelfSigned______"></span><span id="_______selfsigned______"></span><span id="_______SELFSIGNED______"></span> **さまざま**   
この省略可能なエントリは、証明書が記憶域証明書の管理の強化されたツールによって自己署名されているかどうかを指定します。 このエントリが指定されていない場合、ツール、証明書の作成時に証明書に署名します。

**注**  以降 Windows 7 では、NO の値はサポートされていません。 If NO を指定すると、ツールが、エラー メッセージを発行します。

 

<span id="_______ExpirationDate______"></span><span id="_______expirationdate______"></span><span id="_______EXPIRATIONDATE______"></span> **ExpirationDate**   
この必要なエントリでは、証明書の有効期間の末尾を指定します。 証明書が有効期限開始日を指定した有効期限の日付に作成されます。

<span id="_______OrganizationName______"></span><span id="_______organizationname______"></span><span id="_______ORGANIZATIONNAME______"></span> **OrganizationName**   
この省略可能なエントリでは、サブジェクトの証明書を発行する組織の名前を指定します。

<span id="_______OrganizationUnit______"></span><span id="_______organizationunit______"></span><span id="_______ORGANIZATIONUNIT______"></span> **OrganizationUnit**   
この省略可能なエントリでは、サブジェクトの証明書を発行する組織内の部署の名前を指定します。

<span id="_______CompanyLocation______"></span><span id="_______companylocation______"></span><span id="_______COMPANYLOCATION______"></span> **CompanyLocation**   
この省略可能なエントリでは、サブジェクトの証明書を発行する会社の番地を指定します。

<span id="_______State______"></span><span id="_______state______"></span><span id="_______STATE______"></span> **状態**   
この省略可能なエントリでは、サブジェクトの証明書を発行する会社の場所の都道府県を指定します。

<span id="_______ZipCode______"></span><span id="_______zipcode______"></span><span id="_______ZIPCODE______"></span> **郵便番号**   
この省略可能なエントリでは、郵便番号、サブジェクトの証明書を発行する会社の場所を指定します。

<span id="_______Country______"></span><span id="_______country______"></span><span id="_______COUNTRY______"></span> **国**   
この省略可能なエントリでは、サブジェクトの証明書を発行する会社の場所の国/地域を指定します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

証明書のスキーマ ファイルの最初のエントリがある必要があります、 **\[証明書\]** ラベル。

証明書の仕様のエントリは、小文字が区別されますが、任意の順序で指定することができます。

IEEE 1667 準拠 USB 記憶装置にインポートする証明書を作成する方法の詳細については、次を参照してください、 **-新しい**のパラメーター、 [ **/add** ](enhstor-add-switch.md)と[。**置換/** ](-replace-switch.md)拡張記憶域証明書管理ツールのスイッチ。

 

 





