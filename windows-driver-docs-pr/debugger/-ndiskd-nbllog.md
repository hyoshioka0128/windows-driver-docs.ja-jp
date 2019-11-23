---
title: ndiskd ndiskd
description: Ndiskd ndiskd 拡張機能によって、システム上のすべての NBL (NET_BUFFER_LIST) アクティビティのログが表示されます。
ms.assetid: 59CB6B60-E0B3-435E-A6F6-82A715E87C69
keywords:
- ndiskd ndiskd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbllog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0898a87ef75f767eecdb38df4bd3c0f99c04f2ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826619"
---
# <a name="ndiskdnbllog"></a>!ndiskd.nbllog


**! Ndiskd ndiskd**拡張機能によって、システム上のすべての NBL ([**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)) アクティビティのログが表示されます。

```console
!ndiskd.nbllog [-stacks] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-スタック*   
呼び出し履歴を含めます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="remarks"></a>注釈
-------

**重要**  
 **! ndiskd。 ndiskd**では、デバッグ対象ターゲットコンピューターで NBL の追跡が有効になっている必要があります。 NBL の追跡は、Windows のすべての構成で既定で有効になっていません。 NBL tracking が有効になっていない場合は、次のスニペットに示すように、有効にする方法についての説明があります。

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

 

NBL ログには、システム上のネットワークトラフィックが表示されます。 [ **! ndiskd netreport**](-ndiskd-netreport.md)は、NBL 追跡ログを解析して、このネットワークトラフィックを視覚的に表示します。 このため、NBL tracking が有効になっていない場合、 **! ndiskd netreport**はこの情報を表示できません。

<a name="examples"></a>例
--------

ターゲットのデバッグ対象マシンで NBL 追跡を有効にした後、 **! ndiskd ndiskd**コマンドを入力して、システム上のすべての NBL トラフィックのログを確認します。 次の例に示すように、パラメーターを指定せずに **! ndiskd ndiskd**を実行すると、出力は200イベントに制限されます。これは、 *-force*オプションを指定してコマンドを再実行することによってバイパスできます。 この例の出力の中間部分は簡潔にするために excised されています。

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

**! Ndiskd ndiskd**の結果を解釈する方法の詳細については、NDIS ブログの「 [! ndiskd nbl-log](https://go.microsoft.com/fwlink/p/?linkid=846176) 」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[! ndiskd nbl-log](https://go.microsoft.com/fwlink/p/?linkid=846176)

 

 






