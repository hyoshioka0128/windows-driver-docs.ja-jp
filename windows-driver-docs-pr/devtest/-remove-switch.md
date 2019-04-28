---
title: /Remove スイッチ
description: 拡張記憶域証明書管理ツールの/remove と入力しスイッチは、IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ (ASC) の証明書ストアから指定された証明書を削除します。注 IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名のリストを生成し、EhStorCertMgrCmd/List をコマンド プロンプトで入力し、Enter キーを押します。
ms.assetid: c74fe7c3-264e-4bbd-9036-b5a254b3ba5b
keywords:
- /ドライバー開発ツールのスイッチを削除します。
topic_type:
- apiref
api_name:
- /Remove
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fed0152a0c2205763ab058072da62f7162b4758
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361722"
---
# <a name="remove-switch"></a>/Remove スイッチ


**/Remove**拡張記憶域証明書管理ツールのスイッチは、IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ (ASC) の証明書ストアから指定された証明書を削除します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。



```
    EhStorCertMgrCmd /Remove  -Volume:
    VolumeName
     -Index:
    IndexValue
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-ボリューム:**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。



<span id="_______-Index_______"></span><span id="_______-index_______"></span><span id="_______-INDEX_______"></span> **-インデックス:**   
証明書を削除する ASC ストア内のインデックス。 インデックス値は、1 より大きくなければなりません。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/Remove**スイッチは、次の証明書を除く、対象デバイスからすべての証明書を削除します。

-   プロビジョニング証明書 (PCp)。 PCp 証明書を削除するを使用する必要があります、 [ **/Initialize スイッチ**](-initialize-switch.md)します。

-   ASC 製造元証明書 (ASCm)。

    **注**を追加、削除、またはターゲット デバイスに ASC ストアから ASC 製造元 (ASCm) 証明書を置き換えることはできません、記憶域証明書の管理の強化されたツールです。



ターゲット デバイスからの証明書を削除するデバイスする必要がありますプロビジョニングされて PCp の証明書を使っていてデバイスと管理の認証を渡すことができるように、ホストにその証明書の秘密キーが存在する必要があります。

ASC ホストの証明書 (ASCh) を削除する場合、ツールは ASCh 証明書チェーンのすべての関連する署名者証明書 (SCh) を削除します。

ASCh の証明書チェーンから SCh 証明書を削除する場合、ツールは証明書チェーン全体の親 SCh 証明書と共に指定された SCh 証明書を削除します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、ターゲット デバイスの ASC ストア内で 2 つのインデックス位置にある証明書を削除する方法を示します。

```
EhStorCertMgrCmd /Remove -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:2
```









