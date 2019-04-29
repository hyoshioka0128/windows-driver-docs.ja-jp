---
title: ndiskd.nbllog
description: Ndiskd.nbllog 拡張機能は、システム上の NBL (NET_BUFFER_LIST) のすべてのアクティビティのログを表示します。
ms.assetid: 59CB6B60-E0B3-435E-A6F6-82A715E87C69
keywords:
- デバッグ ndiskd.nbllog Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbllog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e6c9563b19f9e2c53287bf424a2bea52f551930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335987"
---
# <a name="ndiskdnbllog"></a>!ndiskd.nbllog


**! Ndiskd.nbllog**拡張機能がすべて NBL のログを表示します ([**NET\_バッファー\_一覧**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)) システム上のアクティビティ。

```console
!ndiskd.nbllog [-stacks] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-履歴*   
呼び出し履歴が含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

**重要な**  
 **! ndiskd.nbllog** NBL の追跡、デバッグ対象のターゲット コンピューターで有効にする必要があります。 NBL の追跡は、Windows のすべての構成で既定では無効です。 NBL の追跡が有効でない場合。 ndiskd が表示されます手順については、有効にする方法については、次のスニペットに示すようにします。

```console
0: kd> !ndiskd.nbllog
    This command requires NBL tracking to be enabled on the debugee target
    machine.  (By default, client operating systems have level 1, and servers
    have level 0).  To enable, set this REG_DWORD value to a nonzero value on
    the target machine and reboot the target machine:
    
    HKLM\SYSTEM\CurrentControlSet\Services\NDIS\Parameters ! TrackNblOwner
    Possible Values (features are cumulative)
    * 0:  Disable all tracking.
    * 1:  Track the most recent owner of each NBL (enables !ndiskd.pendingnbls)
    * 2:  Scan for leaks at runtime (use with StuckNblReaction)
    * 3:  Keep a full history of all activity (enables !ndiskd.nbl -log)
    * 4:  Take stack capture snapshots (enables !ndiskd.nbl -log -stacks)
    This command requires level 3 or higher.
```

 

NBL ログは、システム上のネットワーク トラフィックを表示します。 [**! ndiskd.netreport** ](-ndiskd-netreport.md)視覚的にこのネットワーク トラフィックを表示する NBL 追跡ログを解析します。 そのため、NBL の追跡が有効な場合、 **! ndiskd.netreport**この情報を表示することはできません。

<a name="examples"></a>例
--------

NBL のターゲットのデバッグ対象のマシンで追跡を有効にした後、入力、 **! ndiskd.nbllog**コマンドをシステムに NBL のすべてのトラフィックのログを参照してください。 次の例に示すように実行されている **! ndiskd.nbllog**パラメーターなしでコマンドを再実行することによって回避できますが、200 のイベントへの出力が制限されます、 *-強制*オプション。 この例では、出力の中央が簡潔にするための excised されています。

```console
0: kd> !ndiskd.nbllog
    NBLs               Processor           Event              Detail            
                                                                     
    ffffe00bc71453f0   CPU  0              Freed
    ffffe00bc7163b40   CPU  2              Allocated
    ffffe00bc7163b40   CPU  2              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc7163b40   CPU  2              FilterSent         ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc7163b40   CPU  2, IRQL=DPC    FilterSent         ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc7163b40   CPU  2, IRQL=DPC    SentToMiniport     ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc7163b40   CPU  0, IRQL=DPC    MiniportSendCompleted ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc7163b40   CPU  0, IRQL=DPC    FilterSendCompleted ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc7163b40   CPU  0, IRQL=DPC    FilterSendCompleted send complete in NDIS, sorting to Opens
    ffffe00bc7163b40   CPU  0, IRQL=DPC    SendCompleted      ffffe00bc5ab7c10 - TCPIP6

...

    ffffe00bc6b469b0   CPU  2              Allocated
    ffffe00bc6b469b0   CPU  2              Freed
    ffffe00bc64a3690   CPU  2              Allocated
    ffffe00bc64a3690   CPU  2              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc64a3690   CPU  2              FilterSent         ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc64a3690   CPU  2, IRQL=DPC    FilterSent         ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc64a3690   CPU  2, IRQL=DPC    SentToMiniport     ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc3cf2d10   CPU  1              Allocated
    ffffe00bc7bc6030   CPU  1              Allocated
    ffffe00bc3cf2d10   CPU  1              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000

    Maximum of 200 events printed; quitting early.
    Rerun with the '-force' option to bypass this limit.
```

結果を解釈する方法の詳細な説明の **! ndiskd.nbllog**を参照してください[! ndiskd.nbl-ログ](https://go.microsoft.com/fwlink/p/?linkid=846176)NDIS ブログ。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)

[!ndiskd.nbl -log](https://go.microsoft.com/fwlink/p/?linkid=846176)

 

 






