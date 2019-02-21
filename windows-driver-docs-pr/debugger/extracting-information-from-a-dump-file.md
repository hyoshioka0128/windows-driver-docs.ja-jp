---
title: ダンプ ファイルから情報を抽出
description: ダンプ ファイルから情報を抽出
ms.assetid: abde266e-e3ab-4e5e-ac6d-a27933f3d1a9
keywords:
- ダンプ ファイルから情報を抽出
- ダンプ ファイル、さまざまな情報を抽出
- (ダンプ ファイルから決定する) コンピューター名
- (ダンプ ファイルから決定する) コンピューター名
- (ダンプ ファイルから決定する) の IP アドレス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac63398b42b99a6cedad91bf4ff51041d0f0ba5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537032"
---
# <a name="extracting-information-from-a-dump-file"></a>ダンプ ファイルから情報を抽出


## <span id="ddk_extracting_information_from_a_dump_file_dbg"></span><span id="DDK_EXTRACTING_INFORMATION_FROM_A_DUMP_FILE_DBG"></span>


については、対象のコンピュータの名前などの特定の種類は、ライブ デバッグ中には簡単に使用できます。 ダンプ ファイルをデバッグするときに、この情報を決定するのには少し手間がかかります。

### <a name="span-idfindingthecomputernameinakernelmodedumpfilespanspan-idfindingthecomputernameinakernelmodedumpfilespanfinding-the-computer-name-in-a-kernel-mode-dump-file"></a><span id="finding_the_computer_name_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_COMPUTER_NAME_IN_A_KERNEL_MODE_DUMP_FILE"></span>カーネル モードのダンプ ファイルで、コンピューター名の検索

使用することができます、クラッシュ ダンプが行われたコンピューターの名前を決定する必要がある場合、 [ **! peb** ](-peb.md)拡張機能を探してコンピューター名の値が出力されます。

または、次のコマンドを使用することができます。

```dbgcmd
0: kd> x srv!SrvComputerName
be8ce2e8  srv!SrvComputerName  = _UNICODE_STRING "AIGM-MYCOMP-PUB01"
```

### <a name="span-idfindingtheipaddressinakernelmodedumpfilespanspan-idfindingtheipaddressinakernelmodedumpfilespanfinding-the-ip-address-in-a-kernel-mode-dump-file"></a><span id="finding_the_ip_address_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_IP_ADDRESS_IN_A_KERNEL_MODE_DUMP_FILE"></span>カーネル モードのダンプ ファイル内の IP アドレスの検索

クラッシュ ダンプが行われたコンピューターの IP アドレスを確認するのには、ネットワーク アクティビティをいくつかの送信/受信を表示するスレッドのスタックを検索します。 送信パケットの 1 つを開くか、パケットを受信します。 IP アドレスがそのパケットで表示されます。

### <a name="span-idfindingtheprocessidinausermodedumpfilespanspan-idfindingtheprocessidinausermodedumpfilespanfinding-the-process-id-in-a-user-mode-dump-file"></a><span id="finding_the_process_id_in_a_user_mode_dump_file"></span><span id="FINDING_THE_PROCESS_ID_IN_A_USER_MODE_DUMP_FILE"></span>ユーザー モード ダンプのファイル内のプロセス ID の検索

ユーザー モード ダンプ ファイルから対象アプリケーションのプロセス ID を調べるには、 [ **|(プロセスの状態)** ](---process-status-.md)コマンド。 これにより、ダンプが書き込まれた時点で、デバッグ中のすべてのプロセスが表示されます。 プロセスが一定期間でマークされた (**.**) は、現在のプロセスです。 そのプロセス ID が後に 16 進数で指定された、 **id:** 表記します。

 

 





