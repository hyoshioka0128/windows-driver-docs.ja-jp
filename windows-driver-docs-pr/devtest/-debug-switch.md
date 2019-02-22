---
title: /デバッグ スイッチ
description: 拡張記憶域証明書管理ツールの/Debug スイッチ機能を報告し、IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ証明書 (ASC) に関する情報を格納します。
ms.assetid: 9a7c8fd0-34a8-4f60-a8cb-d5777645f672
keywords:
- /Debug スイッチ ドライバーの開発ツール
topic_type:
- apiref
api_name:
- /Debug
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea6712be11ed34a234460ee6088d2b81c349a40d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559978"
---
# <a name="debug-switch"></a>/デバッグ スイッチ


/**デバッグ**拡張記憶域証明書管理ツールのスイッチ機能と IEEE 1667 準拠 USB ストレージ デバイスに認証サイロ (ASC) の証明書ストアの情報を報告します。 このレポートには、次の部分が含まれます。

-   ハッシュ、署名に使用されるアルゴリズム。

-   証明書のスロットの合計数。

-   占有または空の証明書のスロットの数。

**注**、このトピックを指定した IEEE 1667 準拠している USB ストレージ デバイスを参照として、*ターゲット デバイス*します。



```
    EhStorCertMgrCmd /Debug -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-ボリューム:**   
ターゲット デバイスのボリューム名。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成するために次のように入力します。 **EhStorCertMgrCmd/List** 、コマンドラインから。



### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次の例では、によって生成される出力の抜粋、 **/debug**スイッチします。

```
Execute Debug operation for specified volume name...

Certificate silo device Capabilities...

Certificate Extension Parsing :- 1
Render User Data Unusable :- 1

Hash Algorithm :-
1.3.14.3.2.26
2.16.840.1.101.3.4.2.1
2.16.840.1.101.3.4.2.2
2.16.840.1.101.3.4.2.3

Asymmetric Key Cryptography :-
1.2.840.113549.1.1.1,1024
1.2.840.113549.1.1.1,2048
1.2.840.113549.1.1.1,3072

Signing Algorithm :-
1.2.840.113549.1.1.10,1.3.14.3.2.26
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.1
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.2
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.3
1.3.14.3.2.29
1.2.840.113549.1.1.5
1.2.840.113549.1.1.11
1.2.840.113549.1.1.12
1.2.840.113549.1.1.13

Firmware version :- 1.1

Specification version :- 1.1

Total available slots   :- 16
Occupied slots          :- 3
Free slots              :- 13
```





