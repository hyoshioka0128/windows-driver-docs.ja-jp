---
title: /Clear スイッチ
description: '/Clear スイッチの指定 IEEE 1667 準拠 USB ストレージ デバイスのほとんど (ASC) の証明書認証サイロから証明書の格納、記憶域証明書の管理の強化されたツールを削除します。注: このトピックでは、指定された IEEE 1667 準拠している USB ストレージ デバイスと呼ばれるにターゲット デバイス。'
ms.assetid: b8002d0c-450a-4c4c-bee6-83e382984b34
keywords:
- /オフ スイッチ ドライバーの開発ツール
topic_type:
- apiref
api_name:
- /Clear
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3217f60cad90fa6cc70e59d4489ef405fabad662
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344004"
---
# <a name="clear-switch"></a>/Clear スイッチ


**/Clear**拡張記憶域証明書管理ツールのスイッチが指定された IEEE 1667 準拠 USB ストレージ デバイス認証サイロ (ASC) の証明書ストアから証明書のほとんどを削除します。

**注**、このトピックを指定した IEEE 1667 準拠している USB ストレージ デバイスを参照として、*ターゲット デバイス*します。



```
    EhStorCertMgrCmd /Clear  -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span> **-ボリューム**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/Clear**スイッチは、次の証明書を除く、対象デバイスからすべての証明書をクリアします。

-   プロビジョニング証明書 (PCp)。 PCp 証明書を削除するを使用する必要があります、 [ **/Initialize スイッチ**](-initialize-switch.md)します。

-   ASC 製造元証明書 (ASCm)。

    **注**を追加、削除、またはターゲット デバイスに ASC ストアから ASC 製造元 (ASCm) 証明書を置き換えることはできません、記憶域証明書の管理の強化されたツールです。



ターゲット デバイスからの証明書をオフにするには、デバイスする必要がありますプロビジョニングされて PCp 証明書でいてデバイスと管理の認証に成功するために、ホストでその証明書の秘密キーが存在する必要があります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、ターゲット デバイスからの証明書を削除する方法を示します。

```
EhStorCertMgrCmd /Clear -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```





