---
title: 拡張記憶域証明書管理ツールのコマンド構文
description: 記憶域証明書の管理の強化されたツールは、さまざまなコマンド ライン スイッチを使用して証明書の管理操作を提供します。
ms.assetid: 4b46bdac-77e3-4b73-8942-64d902d53564
keywords:
- 拡張記憶域証明書管理ツールのコマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- Enhanced
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42f94f56ca4a3de83a968ae72e6a78e36b75518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529800"
---
# <a name="enhanced-storage-certificate-management-tool-command-syntax"></a>拡張記憶域証明書管理ツールのコマンド構文


記憶域証明書の管理の強化されたツールは、さまざまなコマンド ライン スイッチを使用して証明書の管理操作を提供します。 各スイッチは、独自のボリューム名と証明書インデックスなどのパラメーターのセットを定義します。

記憶域証明書の管理の強化されたツールはコマンドラインから実行します。

```
    EhStorCertMgrCmd 
    [/Add 
    AddParameters 
    |  

    /Clear 
    ClearParameters
    |

    /Debug 
    DebugParameters
    |

    /Export 
    ExportParameters
    |

    /Help|/?|

    /Initialize 
    InitializeParameters

    |
    /List [
    ListParameters
]| 

    /Remove 
    RemoveParameters
    |

    /Replace 
    ReplaceParameters
    ]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________Add______"></span><span id="________add______"></span><span id="________ADD______"></span> **/追加します。**   
指定された IEEE 1667 準拠 USB ストレージ デバイスの認証サイロ (ASC) の証明書ストアに証明書を追加します。 詳細については、[**追加スイッチ**](enhstor-add-switch.md)を参照してください。

<span id="________Clear______"></span><span id="________clear______"></span><span id="________CLEAR______"></span> **/Clear**   
指定された IEEE 1667 準拠 USB ストレージ デバイス、ASC ストアからすべての証明書を削除します。 詳細については、[ **/Clear スイッチ**](-clear-switch.md)を参照してください。

<span id="________Debug______"></span><span id="________debug______"></span><span id="________DEBUG______"></span> **/Debug**   
機能と IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアに関する情報についてレポートします。 詳細については、[ **/Debug スイッチ**](-debug-switch.md)を参照してください。

<span id="________Export______"></span><span id="________export______"></span><span id="________EXPORT______"></span> **/Export**   
IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアからファイルに指定された証明書をエクスポートします。 このスイッチは、証明書署名要求 (CSR) ファイルへのエクスポートをサポートしています。

詳細については、[ **/Export スイッチ**](-export-switch.md)を参照してください。

<span id="________Help______"></span><span id="________help______"></span><span id="________HELP______"></span> **/Help します。**   
記憶域証明書の管理の強化されたツールの使用状況情報を表示します。 使用して、ヘルプ情報を表示することができます、 **/でしょうか。** スイッチです。

<span id="________Initialize______"></span><span id="________initialize______"></span><span id="________INITIALIZE______"></span> **または初期化**   
その元の製造元の状態に IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアを初期化します。 詳細については、[ **/Initialize スイッチ**](-initialize-switch.md)を参照してください。

<span id="________List______"></span><span id="________list______"></span><span id="________LIST______"></span> **/一覧表示**   
すべての IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに接続を一覧表示します。 このスイッチは、IEEE 1667 準拠 USB ストレージ デバイスに ASC ストア内の証明書を一覧表示することもできます。

詳細については、[ **/List スイッチ**](-list-switch.md)を参照してください。

<span id="________Remove______"></span><span id="________remove______"></span><span id="________REMOVE______"></span> **/Remove**   
IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアから、指定された証明書を削除します。 詳細については、[ **/Remove スイッチ**](-remove-switch.md)を参照してください。

<span id="________Replace______"></span><span id="________replace______"></span><span id="________REPLACE______"></span> **/Replace**   
IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアから指定された証明書を置き換えます。 詳細については、[ **/Replace スイッチ**](-replace-switch.md)を参照してください。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

記憶域証明書の管理の強化されたツールは、追加、削除、または IEEE 1667 準拠 USB ストレージ デバイスに ASC ストアから ASC 製造元 (ASCm) 証明書を置き換えることはできません。 これと他の IEEE 1667 証明書の種類の詳細については、[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)を参照してください。

記憶域証明書の管理の強化されたツールのすべてのスイッチが、スラッシュ (/) のいずれかで開始する必要がありますまたはダッシュ ('-')。 スイッチ パラメーターは、ダッシュ文字で始める必要があります。 スイッチと関連のパラメーターは大文字です。

.









