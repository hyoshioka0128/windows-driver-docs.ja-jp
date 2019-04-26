---
title: /Add スイッチ
description: 記憶域証明書の管理の強化されたツールの/Add スイッチでは、指定した USB デバイスの認証サイロ (ASC) の証明書ストアに証明書を追加します。
ms.assetid: cca064ae-f525-45e4-9778-5fb23efbce88
keywords:
- /ドライバー開発ツールのスイッチを追加します。
topic_type:
- apiref
api_name:
- /Add
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67168f719cd5ed3b9c295b1b8c956143f65df45c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344834"
---
# <a name="add-switch"></a>/Add スイッチ


**/Add**拡張記憶域証明書管理ツールのスイッチが指定された IEEE 1667 準拠 USB ストレージ デバイス認証サイロ (ASC) の証明書ストアに証明書を追加します。

**注**、このトピックでは、指定された IEEE 1667 準拠している USB ストレージ デバイスと呼ばれます、*ターゲット デバイス*します。

 

```
    EhStorCertMgrCmd 
    /Add
     -Volume:
    VolumeName  -Type:CertificateType  -Validation:{None|Basic|Extended} [-Index:IndexValue] [[-Store:Certificate]|[-File:PathToFile]|
[-New:PathToIniFile]]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span> **-ボリューム**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**でコマンド プロンプトを押してから **」と入力**.

 

<span id="_______-Type______"></span><span id="_______-type______"></span><span id="_______-TYPE______"></span> **型**   
追加する証明書の種類、ASC は、ターゲット デバイスに保存します。 次の表では、有効な証明書の種類を定義します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">型の値</th>
<th align="left">説明</th>
<th align="left">インデックス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ASCh</strong></p></td>
<td align="left"><p>認証サイロ証明書 (ASC) は、ホストに証明書認証サイロの認証に使用される証明書をホストします。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>HCh</strong></p></td>
<td align="left"><p>証明書認証サイロへのホストの認証に使用されるホスト証明 (HCh)。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>PCp</strong></p></td>
<td align="left"><p>プロビジョニング証明書 (PCp) のプロビジョニングし、証明書認証サイロを管理する管理者のコマンドのシーケンスで使用されています。</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SCh</strong></p></td>
<td align="left"><p>ホストによって信頼されている証明書を定義するために使用される署名者証明書 (SCh)。 これは、信頼された証明書が ASCh 証明書と 0 個以上の SCh 証明書のチェーン。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-Validation______"></span><span id="_______-validation______"></span><span id="_______-VALIDATION______"></span> **検証**   
ターゲット デバイスでアドレス指定可能なコマンド ターゲット (ACT) によって実行される証明書の検証手順の型。 次の表では、適切な検証の種類を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">検証値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>None</strong></p></td>
<td align="left"><p>証明書は検証されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>基本</strong></p></td>
<td align="left"><p>標準的な IEEE 1667 内で定義されている基本的な検証ポリシーで証明書が検証します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>拡張</strong></p></td>
<td align="left"><p>標準的な IEEE 1667 内で定義されている拡張検証ポリシーで証明書が検証します。</p></td>
</tr>
</tbody>
</table>

 

**注**場合 - 検証: パラメーターが指定されていない、ツールの検証値を使用して**None**します。

 

<span id="_______-Index______"></span><span id="_______-index______"></span><span id="_______-INDEX______"></span> **-インデックス**   
証明書が保存される ASC ストア内のインデックス。 指定したインデックスに、証明書が含まれている場合は、その証明書が置き換えられます。 インデックス値は、0 より大きくなければなりません。

<span id="_______-Store______"></span><span id="_______-store______"></span><span id="_______-STORE______"></span> **ストア**   
ホスト上の証明書ストアに証明書の名前。 証明書ストアに証明書が見つかった場合は、それがターゲット デバイスに追加されます。

詳細については、次を参照してください。 [Windows 証明書ストアから証明書をインポートする](importing-certificates-from-a-windows-certificate-store.md)します。

<span id="_______-File______"></span><span id="_______-file______"></span><span id="_______-FILE______"></span> **-ファイル**   
パスと証明書を含むファイルの名前。 証明書ファイルが見つかると、ツールにより、ターゲット デバイスに追加します。 この証明書で作成された可能性があります、 [ **MakeCert** ](makecert.md)ツールまたは経由でインポート、 [ **/Export スイッチ**](-export-switch.md) Enhanced の記憶域証明書の管理ツールです。

詳細については、次を参照してください。[ファイルから証明書をインポートする](importing-certificates-from-a-file.md)します。

<span id="_______-New______"></span><span id="_______-new______"></span><span id="_______-NEW______"></span> **-新しい**   
パスと、自己署名証明書の作成に使用される仕様を含むファイルの名前。 ファイルが検出された、仕様は有効な場合は、ツール、証明書を作成、デジタル署名、およびターゲット デバイスに証明書を追加します。

詳細については、次を参照してください。 [ **USB ストレージ デバイス用の証明書を作成する**](creating-certificates-for-usb-storage-devices.md)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ターゲット デバイスに証明書を追加すると、次のガイドラインが適用されます。

-   PCp 証明書を使用して、ホストとターゲット デバイスの管理の認証を行います。 ターゲット デバイスには、PCp の証明書があるない場合、は、PCp の証明書でターゲット デバイスを最初にプロビジョニングする必要があります。 PCp 証明書の種類、 **-インデックス**スイッチは、1 つの値を指定する必要があります。

    **重要な**プロビジョニング、PCp のターゲット デバイスに証明書を持つコンピューターに証明書ストアに格納されているその秘密キーのみにすることをお勧めします。 使用して、証明書ストア (を PCp 証明書を含む) をオフにすることができない場合は、ターゲット デバイスに不適切な PCp 証明書がプロビジョニングされると、 [ **/Initialize スイッチ**](-initialize-switch.md)します。

     

-   場合、 **-インデックス**HCh、ASCh を追加して、ツール、SCh 証明書が使用されていない ASC ストア内の最初のインデックスで証明書を格納するときに、スイッチが指定されていません。

    **注**、これらの証明書のターゲット デバイスの種類を追加するには正しい PCp 証明書はデバイスと管理の認証に成功するために存在でホストする必要があります。

     

-   指定したインデックスが、ターゲット デバイスに空でない場合、 **/add**スイッチが指定された証明書に既存の証明書を置き換えます。

    **注**ASCh 証明書チェーン、ツールがすべての関連 SCh を削除します記憶域証明書の管理の強化されたツール ASCh の証明書を指定したインデックス位置にある場合は、します。
    ASCh 証明書チェーンの一部である指定したインデックス位置にある SCh 証明書を代わりに、ツール、ツールは、証明書チェーン内のすべての親 SCh 証明書と共に SCh 証明書を削除します。

     

-   1 つだけ、 **-ストア**、-**ファイル**または **-新しい**パラメーターを指定する必要があります。

**注**を追加、削除、またはターゲット デバイスに ASC ストアから ASC 製造元 (ASCm) 証明書を置き換えることはできません、記憶域証明書の管理の強化されたツールです。

 

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、ターゲット デバイスに、ホストの証明書ストアから証明書を追加する方法を示します。

```
EhStorCertMgrCmd /Add -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:1 -Store:TestCert -Type:PCp -Validation:None
```

 

 





