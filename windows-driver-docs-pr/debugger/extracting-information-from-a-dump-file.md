---
title: ダンプ ファイルからの情報の抽出
description: ダンプ ファイルからの情報の抽出
ms.assetid: abde266e-e3ab-4e5e-ac6d-a27933f3d1a9
keywords:
- ダンプ ファイルから情報を抽出
- ダンプ ファイル、さまざまな情報を抽出
- (ダンプ ファイルから決定する) コンピューター名
- (ダンプ ファイルから決定する) コンピューター名
- (ダンプ ファイルから決定する) の IP アドレス
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 534c208507ed2c07e233984b3a159fac8fc82854
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "57909201"
---
# <a name="extracting-information-from-a-dump-file"></a>ダンプ ファイルからの情報の抽出


## <span id="ddk_extracting_information_from_a_dump_file_dbg"></span><span id="DDK_EXTRACTING_INFORMATION_FROM_A_DUMP_FILE_DBG"></span>


については、対象のコンピュータの名前などの特定の種類は、ライブ デバッグ中には簡単に使用できます。 ダンプ ファイルをデバッグするときに、この情報を決定するのには少し手間がかかります。

### <a name="span-idfindingthecomputernameinakernelmodedumpfilespanspan-idfindingthecomputernameinakernelmodedumpfilespanfinding-the-computer-name-in-a-kernel-mode-dump-file"></a><span id="finding_the_computer_name_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_COMPUTER_NAME_IN_A_KERNEL_MODE_DUMP_FILE"></span>カーネル モードのダンプ ファイルで、コンピューター名の検索

使用することができます、クラッシュ ダンプが行われたコンピューターの名前を決定する必要がある場合、 [ **! peb** ](-peb.md)拡張機能を探してコンピューター名の値が出力されます。

### <a name="span-idfindingtheipaddressinakernelmodedumpfilespanspan-idfindingtheipaddressinakernelmodedumpfilespanfinding-the-ip-address-in-a-kernel-mode-dump-file"></a><span id="finding_the_ip_address_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_IP_ADDRESS_IN_A_KERNEL_MODE_DUMP_FILE"></span>カーネル モードのダンプ ファイル内の IP アドレスの検索

クラッシュ ダンプが行われたコンピューターの IP アドレスを確認するのには、ネットワーク アクティビティをいくつかの送信/受信を表示するスレッドのスタックを検索します。 送信パケットの 1 つを開くか、パケットを受信します。 IP アドレスがそのパケットで表示されます。

### <a name="span-idfindingtheprocessidinausermodedumpfilespanspan-idfindingtheprocessidinausermodedumpfilespanfinding-the-process-id-in-a-user-mode-dump-file"></a><span id="finding_the_process_id_in_a_user_mode_dump_file"></span><span id="FINDING_THE_PROCESS_ID_IN_A_USER_MODE_DUMP_FILE"></span>ユーザー モード ダンプのファイル内のプロセス ID の検索

ユーザー モード ダンプ ファイルから対象アプリケーションのプロセス ID を調べるには、 [ **|(プロセスの状態)** ](---process-status-.md)コマンド。 これにより、ダンプが書き込まれた時点で、デバッグ中のすべてのプロセスが表示されます。 プロセスが一定期間でマークされた (**.**) は、現在のプロセスです。 そのプロセス ID が後に 16 進数で指定された、 **id:** 表記します。

 

 





