---
title: Configuration Manager のコールバック
description: Configuration Manager のコールバック
ms.assetid: a8d33bed-3a06-4d61-be42-b9ae195b79f9
keywords:
- WDK ジョイスティックのコールバック
- configuration manager コールバック WDK ジョイスティック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3ed725d6a60cdad5027d420d2b479a3c6242b834
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390341"
---
# <a name="configuration-manager-callback"></a>Configuration Manager のコールバック





```cpp
CONFIGRET CM_HANDLER CfgRoutine( CONFIGFUNC cfFuncName, 
    SUBCONFIGFUNC scfSubFuncName, DEVNODE dnToDevNode, 
    ULONG dwRefData, ULONG ulFlags );
```

構成マネージャーをやり取りする方法の詳細については、セクション Me、Windows のプラグ アンド プレイの環境の部分で使用可能な Windows ドライバー開発キット (DDK) のです。 (前に、DDK、Windows Driver Kit \[WDK\])。

Configuration manager のコールバックは、VJoyD がコールバックを受け取ると、ミニドライバーは読み込まれる場合にのみ、ミニドライバーに渡されます。 このためは、このコールバックの現在の実装の重要な問題が存在します。 VJoyD はそれが関連付けられている configuration manager デバイスの再構成などの特別なイベントの実行時にメッセージを送信する場合と、システムが、デバイス ノードは、システムのブート時に列挙されたときにそれらのデバイス ノードのコールバックを受け取るを終了します。 そのため、これらのメッセージを受信する時点では、以前起動時に選択されているデバイスのみが読み込まれます。 これにより、ユーザーがシステムを起動します、ジョイスティックを構成、ゲームをプレイ、解除、ジョイスティックを構成してこのコールバックを呼び出すことがなくシャット ダウンため、このコールバックが呼び出されたときに実行される関数の潜在的な数が制限されます。

デバイスのハードウェア リソースが不要の場合、これは問題です。 このようなリソースを使用するデバイスにいくつかのオプションがありますブート時に構成されている場合にのみ動作するように、configuration manager からリソースを動的に割り当てることができますがまたはのレジストリのデバイス ノードの割り当てを検索することができますし、。情報を要求します。

上記の情報を指定するには、ドライバーが正しく初期化いずれかは、ドライバーが最初に読み込まれ、SYS 受信\_動的\_デバイス\_INIT、またはポーリング ルーチンを最初にします。 同様に、リソースが行われるときに、SYS 無料\_動的\_デバイス\_終了メッセージを受信します。

別の問題は、現在サービス ジョイスティック デバイス用のすべての configuration manager コールバックが読み込まれたすべてのミニドライバーに送信されることです。 ただし、使用することができます、 *dnToDevNode*このドライバーを処理できるデバイスに対してこのデバイスの識別子を検索するパラメーターを確認できます。

 

 




