---
title: /Initialize スイッチ
description: /Initialize スイッチでは、その元の製造元の状態に IEEE 1667 準拠 USB ストレージ デバイスでは、認証サイロ (ASC) の証明書ストアを初期化します。
ms.assetid: 4e04a099-8ad6-4eb6-9ac7-d466b7d828d4
keywords:
- /ドライバー開発ツールのスイッチを初期化します。
topic_type:
- apiref
api_name:
- /Initialize
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b49f3b681ac55767f6908c299afb2b95e4ef9f3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574084"
---
# <a name="initialize-switch"></a>/Initialize スイッチ


**/初期化**拡張記憶域証明書管理ツールのスイッチをその元の製造元の状態に IEEE 1667 準拠 USB ストレージ デバイスでは、認証サイロ (ASC) の証明書ストアを初期化します。

**注**、このトピックを指定した IEEE 1667 準拠している USB ストレージ デバイスを参照として、*ターゲット デバイス*します。



```
    EhStorCertMgrCmd /Initialize  -Volume:
    VolumeName 
    [-Quiet]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-ボリューム:**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)を参照してください。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。



<span id="_______-Quiet______"></span><span id="_______-quiet______"></span><span id="_______-QUIET______"></span> **-通知の停止**   
USB ストレージ デバイスの初期化時に、詳細な出力を抑制します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/初期化**スイッチが ASC 製造元 (ASCm) 証明書を除く、ASC ストアからすべての証明書を削除します。 異なり、 [ **/Clear スイッチ**](-clear-switch.md)、 **/初期化**スイッチ ASC ストアからプロビジョニング (PCp) 証明書を削除します。

ターゲット デバイスがプロビジョニング証明書 (PCp) でプロビジョニングされると、その証明書の秘密キーは、デバイスと管理の認証に成功するために、ホスト内に存在する必要があります。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、ターゲット デバイスを初期化する方法を示します。

```
EhStorCertMgrCmd /Initialize -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```









