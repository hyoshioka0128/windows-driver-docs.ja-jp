---
title: PoolMon の要件
description: PoolMon の要件
ms.assetid: 5ee1ed1c-5392-4ce4-8edb-e600b93f82d7
keywords:
- PoolMon WDK、要件
- メモリ プール モニタ WDK の要件
- PoolMon の WDK を表示します
- メモリ プール モニタの WDK を表示します
- WDK PoolMon ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe393b2b7ab5da1a5fcdceefca843d9cea6df178
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326990"
---
# <a name="poolmon-requirements"></a>PoolMon の要件


## <span id="ddk_poolmon_requirements_tools"></span><span id="DDK_POOLMON_REQUIREMENTS_TOOLS"></span>


PoolMon では、次のシステム構成、アクセス許可、およびファイルが必要です。

### <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>システム要件

PoolMon Windows Driver Kit (WDK) で含まれているし、このドキュメントで説明されているのバージョンは、Microsoft Windows XP と Windows の以降のバージョンでのみ実行されます。

### <a name="span-idpooltaggingrequirementspanspan-idpooltaggingrequirementspanspan-idpooltaggingrequirementspanpool-tagging-requirement"></a><span id="Pool_Tagging_Requirement"></span><span id="pool_tagging_requirement"></span><span id="POOL_TAGGING_REQUIREMENT"></span>プールの要件をタグ付け

Windows XP または Windows の以前のバージョンで PoolMon の任意のバージョンを実行する前に、プールのタグ付けを有効にする必要があります。 プールのタグ付けは無期限に Windows Server 2003 および以降のバージョンの Windows で有効にします。

タグ付け機能、プールは、収集し、プールのメモリ割り当てのタグ値で並べ替えることに関する統計を計算します。

プールのタグ付けを有効にするには、GFlags、ツールを Windows のデバッグに含まれるツールを使用します。 開く、**グローバル フラグ** ダイアログ ボックスで、チェック、**プールのタグ付けを有効にする**チェック ボックスをオンして、コンピューターを再起動します。

### <a name="span-idrequirementsforterminalservicessessionpoolmonitoringspanspan-idrequirementsforterminalservicessessionpoolmonitoringspanspan-idrequirementsforterminalservicessessionpoolmonitoringspanrequirements-for-terminal-services-session-pool-monitoring"></a><span id="Requirements_for_Terminal_Services_Session_Pool_Monitoring"></span><span id="requirements_for_terminal_services_session_pool_monitoring"></span><span id="REQUIREMENTS_FOR_TERMINAL_SERVICES_SESSION_POOL_MONITORING"></span>要件のターミナル サービス セッションのプールの監視

PoolMon は、Windows Server 2003 および Windows の以降のバージョンでのみ、ターミナル サービス セッションのプールから割り当てを表示します。

Windows は、コンピューターがターミナル サーバーとして構成されている場合にのみ、ターミナル サービス セッションのプールからメモリを割り当てます。 ターミナル サーバーでは、Win32 サブシステムのカーネル モードの部分は、セッション プールからメモリを割り当てます。 それ以外の場合、Windows は、システムのプールからターミナル サービスのプールのメモリを割り当てます。

### <a name="span-idrequirementsforgeneratingalocaltagfilespanspan-idrequirementsforgeneratingalocaltagfilespanspan-idrequirementsforgeneratingalocaltagfilespanrequirements-for-generating-a-local-tag-file"></a><span id="Requirements_for_Generating_a_Local_Tag_File"></span><span id="requirements_for_generating_a_local_tag_file"></span><span id="REQUIREMENTS_FOR_GENERATING_A_LOCAL_TAG_FILE"></span>ローカル タグ ファイルを生成するための要件

**/C** 、ローカル コンピューター上のドライバーによって使用されるプール タグの localtag.txt ファイルを作成するには、パラメーターは、32 ビット バージョンの Windows でのみサポートされます。

### <a name="span-iddisplayrequirementsspanspan-iddisplayrequirementsspanspan-iddisplayrequirementsspandisplay-requirements"></a><span id="Display_Requirements"></span><span id="display_requirements"></span><span id="DISPLAY_REQUIREMENTS"></span>表示の要件

PoolMon 表示全体を表示するには、コマンド プロンプト ウィンドウのサイズが 80 以上の文字幅をある必要があります (幅 = 80)、少なくとも 53 行の高さ (高さ = 53)、コマンド プロンプト ウィンドウのバッファーが 500 以上の文字幅をする必要があります (幅 = 500) と、少なくとも 2000 行高 (高さ = 2000)。 それ以外の場合、表示は切り捨てられます。

### <a name="span-idrequiredfilesspanspan-idrequiredfilesspanspan-idrequiredfilesspanrequired-files"></a><span id="Required_Files"></span><span id="required_files"></span><span id="REQUIRED_FILES"></span>必要なファイル

poolmon.exe

msdis130.dll

msvcp70.dll

msvcr70.dll

pooltag.txt

 

 





