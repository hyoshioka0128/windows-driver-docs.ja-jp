---
title: /Export スイッチ
description: 記憶域証明書の管理の強化されたツールの/Export スイッチ認証サイロ (ASC) の証明書ストアからファイルに指定された証明書をエクスポートします。
ms.assetid: 00612a63-057a-4ff9-baef-d44de0280cb5
keywords:
- /Export スイッチ ドライバーの開発ツール
topic_type:
- apiref
api_name:
- /Export
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47737642b2140960f35982b761febda96d9da59a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344005"
---
# <a name="export-switch"></a>/Export スイッチ


**/Export**拡張記憶域証明書管理ツールのスイッチは、IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ (ASC) の証明書ストアから指定された証明書をファイルにエクスポートします。 このスイッチは、証明書署名要求 (CSR) ファイルへのエクスポートをサポートしています。

**注**、このトピックを指定した IEEE 1667 準拠している USB ストレージ デバイスを参照として、*ターゲット デバイス*します。

 

```
    EhStorCertMgrCmd
    /Export
     -Volume:
    VolumeName  -Path:PathToFile [-Certificate  -Index:IndexValue [-NoType]] [-Request]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-ボリューム:**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。

 

<span id="_______-Path______"></span><span id="_______-path______"></span><span id="_______-PATH______"></span> **パス**   
完全なパスと、エクスポートした証明書または CSR を含むファイルの名前。

<span id="_______-Certificate_______"></span><span id="_______-certificate_______"></span><span id="_______-CERTIFICATE_______"></span> **-証明書:**   
このスイッチは、証明書のエクスポートが要求されることを指定します。 次のスイッチは、この種の要求と共に使用されます。

<span id="-Index"></span><span id="-index"></span><span id="-INDEX"></span>**-インデックス**  
ターゲット デバイスからの証明書のエクスポート先 ASC ストア内のインデックス。 このスイッチが必要です。

<span id="-NoType"></span><span id="-notype"></span><span id="-NOTYPE"></span>**-NoType**  
ツールを使用して指定されたファイル名に、証明書の種類が追加しない場合、このパラメーターを指定、 **-パス**パラメーター。

このスイッチは省略可能でのみ使用する必要があります、 **-証明書**パラメーター。

<span id="_______-Request______"></span><span id="_______-request______"></span><span id="_______-REQUEST______"></span> **-Request**   
このスイッチは、CSR のエクスポートが要求されることを指定します。 CSR は通常、対象のデバイスにとって、ASC ホスト (ASCh) 証明書を作成する証明機関 (CA) に送信されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

デバイスの ASC ストアから証明書のエクスポートを要求する場合は、インデックスを指定する必要があります。 指定したインデックスに、証明書が含まれていない場合、ツールはエラーを報告します。

場合、 **-証明書**パラメーターを指定すると、ツールは自動的にファイル名で指定された証明書の種類を表す文字列を追加、 **-パス**パラメーター。 次の表では、さまざまな種類の証明書のための文字列を定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">証明書の種類の文字列</th>
<th align="left">説明</th>
<th align="left">インデックス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"ASCm"</p></td>
<td align="left"><p>認証サイロ (ASC) の証明書の製造元。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>"ASCh"</p></td>
<td align="left"><p>ホストに証明書認証サイロの認証に使用される ASC ホスト証明書。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"HCh"</p></td>
<td align="left"><p>証明書認証サイロへのホストの認証に使用されるホストの証明書。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="even">
<td align="left"><p>"PCp"</p></td>
<td align="left"><p>管理コマンドのシーケンスでのプロビジョニングし、証明書認証サイロの管理に使用されるプロビジョニング証明書。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"SCh"</p></td>
<td align="left"><p>署名者証明書をホストによって信頼されている証明書を定義するために使用します。 これは、信頼された証明書が ASCh 証明書と 0 個以上の SCh 証明書のチェーン。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="even">
<td align="left"><p>「が無効です」</p></td>
<td align="left"><p>証明書の種類は、指定したインデックス位置に配置されました。</p></td>
<td align="left"><p>適用なし</p></td>
</tr>
</tbody>
</table>

 

たとえば、PCp 証明書がエクスポート対象のデバイスから、次のコマンドは c: はという名前のファイルを生成します\\MyCertificates\\myCertPCp.cer:。

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

指定した場合、**単純に-notype**パラメーター、 **-証明書**パラメーター、ツールを追加しません証明書の種類の文字列で指定されたファイル名、 **-パス**パラメーター。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、ターゲット デバイスに ASC ストアからインデックス 1 の証明書をエクスポートする方法を示します。

```
EhStorCertMgrCmd /export -Certificate -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Path:c:\MyCertificates\myCert.cer
```

 

 

