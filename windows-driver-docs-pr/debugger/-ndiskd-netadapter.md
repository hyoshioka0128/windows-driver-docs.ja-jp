---
title: ndiskd netadapter
description: Ndiskd netadapter 拡張機能には、システム上でアクティブになっている NDIS ミニポートまたはネットワークアダプターに関する情報が表示されます。
ms.assetid: 7D55F7CE-5DDB-4C80-8C27-F619F2FB7F15
keywords:
- ndiskd netadapter Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b04dfc644c9125e6fd3d43943cbaa37514f4661
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837571"
---
# <a name="ndiskdnetadapter"></a>!ndiskd.netadapter


**! Ndiskd netadapter**拡張機能には、システム上でアクティブになっている NDIS ミニポートまたはネットワークアダプターに関する情報が表示されます。 パラメーターを使用せずにこのコマンドを実行すると、すべてのネットワークアダプターの一覧が表示されます。

```console
     !ndiskd.netadapter [-handle <x>] [-basic] [-diag] [-state] [-bindings] 
        [-ports] [-offloads] [-filterdb] [-timers] [-rst]
        [-pm] [-ss] [-aoac] [-wol] [-protocoloffloads]
        [-rss] [-hw] [-device] [-wmi] [-customwmi]
        [-ndiswmi] [-ref] [-log] [-grovel] [-findname <any>]
        [-rcvfilter] [-nicswitch] [-rcvqueues] [-nicswitches] [-iov]
        [-vfs] [-vports] [-iftrace] [-ip]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
NDIS ミニポートのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
ミニポートに関する概要情報を表示します。

<span id="_______-diag______"></span><span id="_______-DIAG______"></span> *-diag*   
自動診断アラート (存在する場合) を表示します。

<span id="_______-state______"></span><span id="_______-STATE______"></span> *-状態*   
ミニポートの現在の状態を表示します。

<span id="_______-bindings______"></span><span id="_______-BINDINGS______"></span> *-バインド*   
ミニポートバインドを表示します。

<span id="_______-ports______"></span><span id="_______-PORTS______"></span> *-ポート*   
NDIS ポートの一覧を表示します。

<span id="_______-offloads______"></span><span id="_______-OFFLOADS______"></span> *-  のオフロード*  
タスクのオフロードの状態と機能を示します。

<span id="_______-filterdb______"></span><span id="_______-FILTERDB______"></span> *-filterdb*   
現在のパケットフィルターを表示します。

<span id="_______-timers______"></span><span id="_______-TIMERS______"></span> *-タイマー*   
ミニポートによって割り当てられたタイマーオブジェクトを表示します。

<span id="_______-rst______"></span><span id="_______-RST______"></span> *-rst*   
受信側の制限の状態を表示します。

<span id="_______-pm______"></span><span id="_______-PM______"></span> *-pm*   
電源管理の状態と機能を表示します。

<span id="_______-ss______"></span><span id="_______-SS______"></span> *-ss*   
セレクティブサスペンドの状態を表示します。

<span id="_______-aoac______"></span><span id="_______-AOAC______"></span> *-電源*   
接続スタンバイ状態を示します。

<span id="_______-wol______"></span><span id="_______-WOL______"></span> *-wol*   
Wake on LAN (WoL) 構成を示します。

<span id="_______-protocoloffloads______"></span><span id="_______-PROTOCOLOFFLOADS______"></span> *-protocoloffloads*   
アクティブな電源管理プロトコルのオフロードを示します。

<span id="_______-rss______"></span><span id="_______-RSS______"></span> *-rss*   
受信側のスケーリングパラメーターを示します。

<span id="_______-hw______"></span><span id="_______-HW______"></span> *-hw*   
ハードウェアリソースが表示されます。

<span id="_______-device______"></span><span id="_______-DEVICE______"></span> *-デバイスの*   
基になる NT デバイスオブジェクトに関する情報を表示します。

<span id="_______-wmi______"></span><span id="_______-WMI______"></span> *-wmi*   
アダプターに登録されている WMI Guid を表示します。

<span id="_______-customwmi______"></span><span id="_______-CUSTOMWMI______"></span> *-customwmi*   
ミニポートによって登録されたカスタム WMI Guid を表示します。

<span id="_______-ndiswmi______"></span><span id="_______-NDISWMI______"></span> *-ndiswmi*   
NDIS によって提供される WMI Guid を示します。

<span id="_______-ref______"></span><span id="_______-REF______"></span> *-ref*   
ミニポートの参照の内訳を表示します。

<span id="_______-log______"></span><span id="_______-LOG______"></span> *-ログ*   
PnP および電源イベントログを表示します。

<span id="_______-grovel______"></span><span id="_______-GROVEL______"></span> *-grovel*   
メモリ内のミニポートブロックを強制的に検索します。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
ミニポートを名前プレフィックスでフィルター処理します。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span> *-rcvfilter*   
受信フィルター処理機能を示します。

<span id="_______-nicswitch______"></span><span id="_______-NICSWITCH______"></span> *-nicswitch*   
NIC スイッチの機能を示します。

<span id="_______-rcvqueues______"></span><span id="_______-RCVQUEUES______"></span> *-rcvqueues*   
受信キューを表示します。

<span id="_______-nicswitches______"></span><span id="_______-NICSWITCHES______"></span> *-nicswitches*   
NIC スイッチを表示します。

<span id="_______-iov______"></span><span id="_______-IOV______"></span> *-sr-iov*   
SR-IOV (シングルルート i/o 仮想化) 機能を示します。

<span id="_______-vfs______"></span><span id="_______-VFS______"></span> *-vfs*   
Sr-iov の VFs (仮想フィルター) を示します。

<span id="_______-vports______"></span><span id="_______-VPORTS______"></span> *-vports*   
Vports (仮想ポート) を表示します。

<span id="_______-ifrtrace______"></span><span id="_______-IFRTRACE______"></span> *-ifrtrace*   
インフライトレコーダーのトレースを表示します。

<span id="_______-ip______"></span><span id="_______-IP______"></span> *-ip*   
ネットワークのインターフェイスの IP アドレスを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

パラメーターを使用せずに **! ndiskd netadapter**を実行すると、システム上のすべてのネットワークアダプターの一覧と、関連するミニポートドライバーを取得できます。 この例の出力では、ffffdf80140c71a0 というハンドルを持つ Microsoft カーネルデバッグネットワークアダプターを探しています。 カーネルデバッグネットワークアダプターの詳細については、NDIS ブログの「[ネットワーク経由でのカーネルデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845868)」を参照してください。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffdf8015a98380   ffffdf8015aa11a0    Microsoft ISATAP Adapter #2
    ffffdf801418d650   ffffdf80140c71a0    Microsoft Kernel Debug Network Adapter
```

ミニポートドライバーのハンドルをクリックするか、 **! ndiskd ハンドル**を入力することで、そのデバイス上のすべての NDIS の状態を確認できるようになりました。 これは、ネットワークドライバーのトラブルシューティングを行う場合や、ネットワークスタック内で問題が発生している場所を調べる場合に役立ちます。 たとえば、ドライバーのデータパスの状態を確認して、接続されているかどうかを確認できます。

このネットアダプターのレポートの下部には、他にも多数のリンクがあります。これをクリックすると、保留中の Oid やタスクのオフロードの状態などの詳細情報を確認できます。 これらのリンクは、 **! ndiskd netadapter**のパラメーターの多くに対応しています。

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

さらにデバッグするための開始位置として **! ndiskd netadapter**を使用する例として、レポートの下部にある [ドライバーハンドラー] リンクをクリックして、このネットアダプターのミニポートドライバーのすべての登録済みドライバーコールバックハンドラーの一覧を表示します。 次の例では、リンクをクリックすると、このネットアダプターのミニポートドライバーのハンドルを使用して! ndiskd[**ミニドライバー**](-ndiskd-minidriver.md)拡張機能が実行されます。 ミニポートドライバーは kdnic 4.2 で、ハンドルは ffffdf801418d650 です。

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

各ハンドラーの右側にある "bp" リンクをクリックして、特定の問題をデバッグするハンドラーにブレークポイントを設定できるようになりました。 たとえば、データパスにハングがある場合は、ドライバーの SendNetBufferListsHandler または ReturnNetBufferListsHandler を調べることができます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[ネットワーク経由でのカーネルデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845868)

[ **! ndiskd ミニドライバー**](-ndiskd-minidriver.md)










