---
title: /スイッチを置換します。
description: 記憶域証明書の管理の強化されたツールの/Replace スイッチには、デバイスに認証サイロ (ASC) の証明書ストアから証明書が置き換えられます。
ms.assetid: 8fbdeb88-ec38-4ffc-a669-83fd612819ed
keywords:
- /スイッチ ドライバーの開発ツールを置換します。
topic_type:
- apiref
api_name:
- /Replace
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 636891f8495724145fd65d546000b210dfafa246
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559777"
---
# <a name="replace-switch"></a>/スイッチを置換します。


**置換/** 拡張記憶域証明書管理ツールのスイッチには、IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ (ASC) の証明書ストアから指定された証明書が置き換えられます。

**注**  、このトピックを指定した IEEE 1667 準拠している USB ストレージ デバイスを参照として、*ターゲット デバイス*します。

 

```
    EhStorCertMgrCmd 
    /Replace 
    -Volume:
    VolumeName  -Type:CertificateType  [-Validation:{None|Basic|Extended}] [-Index:IndexValue] [[-Store:Certificate]|[-File:PathToFile]|[-New:PathToIniFile]]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span> **-ボリューム**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**  IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで、キーを押します入力します。

 

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
<td align="left"><p>証明書認証サイロへのホストの認証に使用されるホストの証明書。</p></td>
<td align="left"><p>インデックスを 1 より大きい場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SCh</strong></p></td>
<td align="left"><p>署名者証明書をホストによって信頼されている証明書を定義するために使用します。 これは、信頼された証明書が ASCh 証明書と 0 個以上の SCh 証明書のチェーン。</p></td>
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
<td align="left"><p><strong>なし</strong></p></td>
<td align="left"><p>証明書は検証されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>基本的な</strong></p></td>
<td align="left"><p>証明書は、標準的な IEEE 1667 内で定義されている基本的な検証ポリシーを使用して検証します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>拡張</strong></p></td>
<td align="left"><p>証明書は、標準的な IEEE 1667 内で定義されている拡張検証ポリシーを使用して検証します。</p></td>
</tr>
</tbody>
</table>

 

**注**  場合 - 検証: パラメーターが指定されていない、ツールの検証値を使用して**None**します。

 

<span id="_______-Index______"></span><span id="_______-index______"></span><span id="_______-INDEX______"></span> **-インデックス**   
証明書が置き換えられます ASC ストア内のインデックス。 インデックス値は、1 より大きくなければなりません。

**注**  ターゲット デバイスに指定したインデックス位置にある証明書が存在する必要があります。

 

<span id="_______-Store______"></span><span id="_______-store______"></span><span id="_______-STORE______"></span> **ストア**   
ホスト上の証明書ストアに証明書の名前。 証明書ストアに証明書が見つかった場合は、それがターゲット デバイスに追加されます。

詳細については、次を参照してください。 [Windows 証明書ストアから証明書をインポートする](importing-certificates-from-a-windows-certificate-store.md)します。

<span id="_______-File______"></span><span id="_______-file______"></span><span id="_______-FILE______"></span> **-ファイル**   
パスと証明書を含むファイルの名前。 証明書ファイルが見つかると、ツールにより、ターゲット デバイスに追加します。 MakeCert ツールを使用して作成またはインポートを使用してこの証明書がでした、 [ **/Export スイッチ**](-export-switch.md)の記憶域証明書の管理の強化されたツールです。

詳細については、次を参照してください。[ファイルから証明書をインポートする](importing-certificates-from-a-file.md)します。

<span id="_______-New______"></span><span id="_______-new______"></span><span id="_______-NEW______"></span> **-新しい**   
パスと、自己署名証明書の作成に使用される仕様を含むファイルの名前。 ファイルが検出された、仕様は有効な場合は、ツール、証明書を作成、デジタル署名、およびターゲット デバイスに証明書を追加します。

詳細については、次を参照してください。 [ **USB ストレージ デバイス用の証明書を作成する**](creating-certificates-for-usb-storage-devices.md)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**置換/** スイッチを使用すると、次の証明書を除く、対象デバイスから任意の証明書を置き換えます。

-   プロビジョニング証明書 (PCp)。 使用する必要があります、PCp の証明書を置換する、 [ **/Initialize スイッチ**](-initialize-switch.md)します。

-   ASC 製造元証明書 (ASCm)。

    **注**  追加、削除、またはターゲット デバイスに ASC ストアから ASCm 証明書を置き換えることはできません、記憶域証明書の管理の強化されたツールです。

     

ターゲット デバイスに証明書を置換するデバイスする必要がありますがプロビジョニングされて PCp 証明書でいてデバイスと管理の認証を渡すことができるように、ホストにその証明書の秘密キーが存在する必要があります。

ASCh の証明書を交換する場合、ツールは ASCh 証明書チェーンのすべての関連 SCh を削除します。

ASCh の証明書チェーンから SCh 証明書を交換する場合、ツールは証明書チェーン内のすべての親 SCh 証明書と共に指定された SCh 証明書を削除します。

1 つだけ、 **-ストア**、 **-ファイル**または **-新しい**パラメーターを指定する必要があります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、IEEE 1667 準拠 USB 記憶装置の ASC ストア内で 2 つのインデックス位置にある証明書を置換する方法を示します。

```
EhStorCertMgrCmd /Replace -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:2 -Store:TestCert -Type:SCh -Validation:None
```

 

 





