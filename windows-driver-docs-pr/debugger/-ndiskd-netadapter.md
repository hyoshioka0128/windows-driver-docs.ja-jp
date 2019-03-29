---
title: ndiskd.netadapter
description: Ndiskd.netadapter 拡張機能では、NDIS ミニポート、またはシステムでアクティブなネットワーク アダプターに関する情報が表示されます。
ms.assetid: 7D55F7CE-5DDB-4C80-8C27-F619F2FB7F15
keywords:
- デバッグ ndiskd.netadapter Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c693ace3df2b1f1be9d9b39e4cab34fef6ca870
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573154"
---
# <a name="ndiskdnetadapter"></a>!ndiskd.netadapter


**! Ndiskd.netadapter**拡張機能は、NDIS ミニポート、またはシステムでアクティブなネットワーク アダプターに関する情報を表示します。 パラメーターなしで、このコマンドを実行する場合。 ndiskd すべてのネットワーク アダプターの一覧が表示されます。

```console
     !ndiskd.netadapter [-handle <x>] [-basic] [-diag] [-state] [-bindings] 
        [-ports] [-offloads] [-filterdb] [-timers] [-rst]
        [-pm] [-ss] [-aoac] [-wol] [-protocoloffloads]
        [-rss] [-hw] [-device] [-wmi] [-customwmi]
        [-ndiswmi] [-ref] [-log] [-grovel] [-findname <any>]
        [-rcvfilter] [-nicswitch] [-rcvqueues] [-nicswitches] [-iov]
        [-vfs] [-vports] [-iftrace] [-ip]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS ミニポートのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
ミニポートに関する概要情報が表示されます。

<span id="_______-diag______"></span><span id="_______-DIAG______"></span> *-診断*   
自動診断アラートが表示されます (ある場合)。

<span id="_______-state______"></span><span id="_______-STATE______"></span> *-state*   
ミニポートの現在の状態を表示します。

<span id="_______-bindings______"></span><span id="_______-BINDINGS______"></span> *-バインド*   
ミニポート バインドを表示します。

<span id="_______-ports______"></span><span id="_______-PORTS______"></span> *-ポート*   
NDIS ポートの一覧が表示されます。

<span id="_______-offloads______"></span><span id="_______-OFFLOADS______"></span> *負荷を軽減*   
タスクのオフロード状態と機能を示します。

<span id="_______-filterdb______"></span><span id="_______-FILTERDB______"></span> *-filterdb*   
現在のパケット フィルターを示しています。

<span id="_______-timers______"></span><span id="_______-TIMERS______"></span> *-タイマー*   
ミニポートによって割り当てられたタイマー オブジェクトを示しています。

<span id="_______-rst______"></span><span id="_______-RST______"></span> *-rst*   
受信側の制限の状態を示しています。

<span id="_______-pm______"></span><span id="_______-PM______"></span> *-pm*   
電源管理の状態と機能を示しています。

<span id="_______-ss______"></span><span id="_______-SS______"></span> *-ss*   
セレクティブ サスペンド状態を示しています。

<span id="_______-aoac______"></span><span id="_______-AOAC______"></span> *-aoac*   
AOAC (コネクト スタンバイ) の状態を示しています。

<span id="_______-wol______"></span><span id="_______-WOL______"></span> *-wol*   
Wake on LAN (WoL) の構成を示します。

<span id="_______-protocoloffloads______"></span><span id="_______-PROTOCOLOFFLOADS______"></span> *-protocoloffloads*   
アクティブな電源管理プロトコルの表示をオフロードします。

<span id="_______-rss______"></span><span id="_______-RSS______"></span> *-rss*   
Receive Side Scaling のパラメーターを示します。

<span id="_______-hw______"></span><span id="_______-HW______"></span> *-hw*   
ハードウェア リソースが表示されます。

<span id="_______-device______"></span><span id="_______-DEVICE______"></span> *-device*   
基になる NT デバイス オブジェクトに関する情報が表示されます。

<span id="_______-wmi______"></span><span id="_______-WMI______"></span> *-wmi*   
アダプターに登録されている WMI の Guid を示しています。

<span id="_______-customwmi______"></span><span id="_______-CUSTOMWMI______"></span> *-customwmi*   
ミニポートによって登録されているカスタムの WMI Guid を示しています。

<span id="_______-ndiswmi______"></span><span id="_______-NDISWMI______"></span> *-ndiswmi*   
NDIS で提供される WMI の Guid を示しています。

<span id="_______-ref______"></span><span id="_______-REF______"></span> *-ref*   
ミニポートには、参照の内訳を示します。

<span id="_______-log______"></span><span id="_______-LOG______"></span> *-log*   
PnP と電力のイベント ログを表示します。

<span id="_______-grovel______"></span><span id="_______-GROVEL______"></span> *-grovel*   
メモリ内を検索するミニポートのブロックを強制的にします。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
ミニポートを名のプレフィックスでフィルター処理します。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span> *-rcvfilter*   
表示には、フィルター処理機能が表示されます。

<span id="_______-nicswitch______"></span><span id="_______-NICSWITCH______"></span> *-nicswitch*   
NIC のスイッチ機能を示しています。

<span id="_______-rcvqueues______"></span><span id="_______-RCVQUEUES______"></span> *-rcvqueues*   
表示には、キューが表示されます。

<span id="_______-nicswitches______"></span><span id="_______-NICSWITCHES______"></span> *-nicswitches*   
NIC のスイッチを示します。

<span id="_______-iov______"></span><span id="_______-IOV______"></span> *-iov*   
SR-IOV (Single Root I/O Virtualization) 機能を示しています。

<span id="_______-vfs______"></span><span id="_______-VFS______"></span> *-vfs*   
SR-IOV Vf (仮想フィルター) を示しています。

<span id="_______-vports______"></span><span id="_______-VPORTS______"></span> *-拡張*   
拡張 (仮想ポート) を示しています。

<span id="_______-ifrtrace______"></span><span id="_______-IFRTRACE______"></span> *-ifrtrace*   
実行中のレコーダーのトレースを示しています。

<span id="_______-ip______"></span><span id="_______-IP______"></span> *ip アドレス*   
ネットワークのインターフェイスで IP アドレスを示しています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

実行して **! ndiskd.netadapter**パラメーターなしで、関連付けられているミニポート ドライバーと共にシステム上ですべてのネットワーク アダプターの一覧を取得することができます。 この出力の例では、Microsoft カーネル デバッグ ネットワーク アダプターが、そのハンドルは ffffdf80140c71a0 を探します。 カーネル デバッグ ネットワーク アダプターに関する詳細については、次を参照してください。[ネットワーク経由でのカーネル デバッグ](https://go.microsoft.com/fwlink/p/?linkid=845868)NDIS ブログ。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffdf8015a98380   ffffdf8015aa11a0    Microsoft ISATAP Adapter #2
    ffffdf801418d650   ffffdf80140c71a0    Microsoft Kernel Debug Network Adapter
```

ミニポート ドライバーのハンドルをクリックするか入力して、 **! ndiskd.netadapter-処理**、そのデバイスで参照すべて NDIS の状態のようになりました。 トラブルシューティングのネットワーク ドライバーまたはネットワーク スタックに問題がある場合を把握するための出発点として非常に便利なことができます。 たとえば、ドライバーのデータパス状態を確認でき、か接続されているかどうかを参照してください。

このネット アダプターのレポートの下部にある、他のリンクが多数など、保留中の Oid の詳細情報を調べたりをクリックすることができ、タスクの状態の負荷を軽減します。 これらのリンクは、多くのパラメーターの対応 **! ndiskd.netadapter**します。

```console
3: kd> !ndiskd.netadapter ffffdf80140c71a0


MINIPORT

    Microsoft Kernel Debug Network Adapter

    Ndis handle        ffffdf80140c71a0
    Ndis API version   v6.20
    Adapter context    ffffdf80147d7230
    Driver             ffffdf801418d650 - kdnic  v4.2
    Network interface  ffffdf80139b3a20

    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Device instance    ROOT\KDNIC\0000
    Device object      ffffdf80140c7050    More information
    MAC address        18-03-73-c1-e8-72


STATE

    Miniport           Running
    Device PnP         Started             Show state history
    Datapath           Normal
    Interface          Up
    Media              Connected
    Power              D0
    References         0n10                Show detail
    Total resets       0
    Pending OID        None
    Flags              NOT_BUS_MASTER, ALLOW_BUGCHECK_CALLBACK,
                       BUGCHECK_CALLBACK_REGISTERED, DEFAULT_PORT_ACTIVATED,
                       SUPPORTS_MEDIA_SENSE, DOES_NOT_DO_LOOPBACK,
                       MEDIA_CONNECTED
    PnP flags          VIRTUAL_DEVICE, HIDDEN, NO_HALT_ON_SUSPEND,
                       RECEIVED_START


BINDINGS

    Protocol list      Driver              Open               Context           
    MSLLDP             ffffdf80120a5c10    ffffdf8015a749c0   ffffdf8015d325e0
    TCPIP              ffffdf80131cc010    ffffdf801494a650   ffffdf801494aa50
    NDISUIO            ffffdf8015a58140    ffffdf8015a78c10   ffffdf8015a77e00
    TCPIP6             ffffdf80131c9c10    ffffdf80147875a0   ffffdf801494f010
    (RASPPPOE)         Not running
    RSPNDR             ffffdf80120a0c10    ffffdf8015a79c10   ffffdf8015a79010
    LLTDIO             ffffdf8015a5f9b0    ffffdf801406f010   ffffdf8015a786c0
    (RDMANDK)          ffffdf801406d8f0    Declined with NDIS_STATUS_NOT_RECOGNIZED

    Filter list        Driver              Module             Context           
    WFP 802.3 MAC Layer LightWeight Filter-0000
                       ffffdf80139a5a70    ffffdf801494c670   ffffdf801494a010
    QoS Packet Scheduler-0000
                       ffffdf8014039d90    ffffdf801494dc70   ffffdf80147dc2b0
    WFP Native MAC Layer LightWeight Filter-0000
                       ffffdf80139fcd70    ffffdf8014950c70   ffffdf8014950880



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs                           Timers
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
    Hardware resources                     Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

使用例として **! ndiskd.netadapter**さらにデバッグするための出発点としてこのネット アダプターのミニポートのすべての登録済みのドライバーのコールバック ハンドラーの一覧を表示するレポートの下部にある「ドライバー ハンドラー」リンクをクリックします。ドライバー。 次の例では、リンクをクリックすると、! ndiskd を実行する、 [ **! ndiskd.minidriver** ](-ndiskd-minidriver.md)このネット アダプターのミニポート ドライバーのハンドルを持つ拡張機能。 ミニポート ドライバーが kdnic 4.2 とそのハンドルは ffffdf801418d650 します。

```console
3: kd> !ndiskd.minidriver ffffdf801418d650 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80f1fd78230  bp
    SetOptionsHandler                      fffff80f1fd72800  bp
    HaltHandlerEx                          fffff80f1fd78040  bp
    ShutdownHandlerEx                      fffff80f1fd722c0  bp

    CheckForHangHandlerEx                  fffff80f1fd72810  bp
    ResetHandlerEx                         fffff80f1fd72f70  bp

    PauseHandler                           fffff80f1fd78000  bp
    RestartHandler                         fffff80f1fd78940  bp

    OidRequestHandler                      fffff80f1fd71c90  bp
    CancelOidRequestHandler                fffff80f1fd722c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80f1fd789a0  bp

    SendNetBufferListsHandler              fffff80f1fd71870  bp
    ReturnNetBufferListsHandler            fffff80f1fd71b50  bp
    CancelSendHandler                      fffff80f1fd722c0  bp
```

特定の問題をデバッグするには、そのハンドラーにブレークポイントを設定する各ハンドラーの右側に"bp"リンクをクリックすることができますようになりました。 たとえば、データパス ハングがある場合は、ドライバーの SendNetBufferListsHandler または ReturnNetBufferListsHandler を調査できます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[カーネルは、ネットワーク経由でのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845868)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)










