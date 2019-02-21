---
title: PortCls オーディオ ドライバーの PnP 実装を再調整します。
description: PnP 再調整はシナリオで使用特定 PCI を再割り当てするメモリ リソースが必要があります。
ms.assetid: FCAD7F8B-AA9B-430A-BCAF-04E13FA15382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0881661fb05211711bfcb13845fd748293d7fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537865"
---
# <a name="implement-pnp-rebalance-for-portcls-audio-drivers"></a>PortCls オーディオ ドライバーの PnP 実装を再調整します。


PnP 再調整はシナリオで使用特定 PCI を再割り当てするメモリ リソースが必要があります。

2 つの主なシナリオでは、再調整が引き起こされます。

1. PCI ホットプラグ:ユーザーはデバイスをプラグインし、PCI バスには、新しいデバイスのドライバーの読み込みには、十分なリソースはありません。 このカテゴリに分類されるデバイスのいくつかの例には、Thunderbolt、USB C および NVME ストレージが含まれます。 このシナリオのメモリ リソースしなければ再配置し、統合 (rebalanced) 追加される追加のデバイスをサポートします。
2. PCI サイズ バー:デバイスのドライバーのメモリに読み込みが成功した後、その他のリソースを要求します。 デバイスのいくつかの例には、ハイエンドなグラフィックス カードと記憶装置が含まれます。 詳細については、ビデオ ドライバーのサポートの「[上サイズ変更バー サポート](https://msdn.microsoft.com/library/windows/hardware/dn894179)します。
このトピックでは、PortCls オーディオ ドライバーの PnP 再調整を実装するために必要な内容について説明します。

PnP は均衡が Windows 10、バージョン 1511 以降のバージョンの Windows で使用できます。

## <a name="span-idrebalancerequirementsspanspan-idrebalancerequirementsspanspan-idrebalancerequirementsspanrebalance-requirements"></a><span id="Rebalance_Requirements"></span><span id="rebalance_requirements"></span><span id="REBALANCE_REQUIREMENTS"></span>要件のバランスを再調整します。


Portcls オーディオ ドライバーには、次の条件が満たされた場合に再調整をサポートする機能があります。

-   ミニポートを登録する必要があります、 [IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850) Portcls と連携します。
-   ミニポートから PcRebalanceRemoveSubdevices を返す必要があります[ **IAdapterPnpManagement::GetSupportedRebalanceType**](https://msdn.microsoft.com/library/windows/hardware/mt604851)します。
-   トポロジと WaveRT はサポートされている 2 つのポートの種類です。

アクティブなオーディオ ストリームがある場合に再調整をサポートするために、portcls オーディオ ドライバーは、これら 2 つの追加要件の 1 つを満たす必要があります。

-   ドライバーでは、 [ **IMiniportWaveRTInputStream::GetReadPacket** ](https://msdn.microsoft.com/library/windows/hardware/dn946533)と[IMiniportWaveRTOutputStream](https://msdn.microsoft.com/library/windows/hardware/dn946534)オーディオ ストリームのパケットのインターフェイス。 このオプションを選択することをお勧めします。

または

-   ドライバーをサポートしていない場合は、get/書き込み IMiniportWaveRT ストリームでドライバーをサポートする必要がありますいない[ **KSPROPERTY\_RTAUDIO\_POSITIONREGISTER** ](https://msdn.microsoft.com/library/windows/hardware/ff537381)と[ **KSPROPERTY\_RTAUDIO\_CLOCKREGISTER**](https://msdn.microsoft.com/library/windows/hardware/ff537376)します。 オーディオ エンジンを使用して、 [ **IMiniportWaveRTStream::GetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff536749)このシナリオでは。

## <a name="span-idaudiostreambehaviorwhenrebalancingoccursspanspan-idaudiostreambehaviorwhenrebalancingoccursspanspan-idaudiostreambehaviorwhenrebalancingoccursspanaudio-stream-behavior-when-rebalancing-occurs"></a><span id="Audio_Stream_Behavior_When_Rebalancing_Occurs"></span><span id="audio_stream_behavior_when_rebalancing_occurs"></span><span id="AUDIO_STREAM_BEHAVIOR_WHEN_REBALANCING_OCCURS"></span>再調整が発生したとき、オーディオ Stream 動作


再調整がトリガーされる場合は、作業中のオーディオ ストリームがあるし、アクティブなオーディオ ストリームのサポートを再調整し、すべてのアクティブなオーディオ ストリームは停止され自動的に再起動されませんが、ドライバーが提供されます。

## <a name="span-idiportclspnpcominterfacespanspan-idiportclspnpcominterfacespanspan-idiportclspnpcominterfacespaniportclspnp-com-interface"></a><span id="IPortClsPnp_COM_Interface"></span><span id="iportclspnp_com_interface"></span><span id="IPORTCLSPNP_COM_INTERFACE"></span>IPortClsPnp COM インターフェイス


`IPortClsPnp` ポート クラス ドライバー (PortCls) がアダプターに公開する管理インターフェイスは、PnP です。

`IPortClsPnp` 継承**IUnknown**も、次のメソッドをサポートしています。

-   [**IPortClsPnp::RegisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604860)
-   [**IPortClsPnp::UnregisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604861)

オーディオのミニポート ドライバーが Portcls エクスポートを使用して、PNP 通知インターフェイスを登録またはを使用して、 [ **IPortClsPnp** ](https://msdn.microsoft.com/library/windows/hardware/mt604859) COM インターフェイス IPortClsPnp WaveRT ポートのオブジェクトで公開します。 使用[ **IPortClsPnp::RegisterAdapterPnpManagement** ](https://msdn.microsoft.com/library/windows/hardware/mt604860)と[ **IPortClsPnp::UnregisterAdapterPnpManagement** ](https://msdn.microsoft.com/library/windows/hardware/mt604861)を登録して登録を解除します。

## <a name="span-idrequiredportclsexportddisspanspan-idrequiredportclsexportddisspanspan-idrequiredportclsexportddisspanrequired-portcls-export-ddis"></a><span id="Required_PortCls_Export_DDIs"></span><span id="required_portcls_export_ddis"></span><span id="REQUIRED_PORTCLS_EXPORT_DDIS"></span>必須の PortCls エクスポート Ddi


[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850)インターフェイス アダプターの実装および PnP 管理メッセージを受信する場合を登録する必要があります。 このインターフェイスに登録 PortCls を使用して[ **PcRegisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604865)します。 このインターフェイスを PortCls を使用して登録を解除[ **PcUnregisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604866)します。

## <a name="span-idrequireddriverddisspanspan-idrequireddriverddisspanspan-idrequireddriverddisspanrequired-driver-ddis"></a><span id="Required_Driver_DDIs"></span><span id="required_driver_ddis"></span><span id="REQUIRED_DRIVER_DDIS"></span>必要なドライバー Ddi


次[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850) Ddi を再調整をサポートするために実装する必要があります。

-   [**IAdapterPnpManagement::GetSupportedRebalanceType** ](https://msdn.microsoft.com/library/windows/hardware/mt604851) Portcls によってする処理中に呼び出されます。 定義されているミニポートがサポートされている再調整の種類を返します、 [ **PC\_を再調整\_型**](https://msdn.microsoft.com/library/windows/hardware/mt604867)列挙型。

    **注**  Portcls 呼び出しの前に、デバイスのグローバル ロックの取得、したがってミニポートがする必要がありますこの呼び出しをできるだけ高速実行します。

     

-   [**IAdapterPnpManagement::PnpQueryStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604853)する IRP の次の位置の直前に portcls が呼び出されます。 これは通知だけであり、呼び出しは値を返しません。

    **注**  Portcls 呼び出しの前に、デバイスのグローバル ロックの取得、したがってミニポートがする必要がありますこの呼び出しをできるだけ高速実行します。 Portcls が (保留) をブロックする停止は保留中ですが、いずれかの新しい要求を作成します。

     

-   [**IAdapterPnpManagement::PnpCancelStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604852) CanceStop IRP の処理中に portcls が呼び出されます。 これは、通知だけです。 ミニポート以前 PnpQueryStop 通知を受信しなくても PnpCancelStop を受信することができます。 この動作を対応するために、ミニポートが書き込まれます。 たとえば、これは、場合 Portcls がある営業案件、ミニポートにこの通知を転送する前にするロジックは IRP が失敗した場合。 このシナリオでは、PnP キャンセル Stop を PnP マネージャーはまだ呼び出します。

    **注**  Portcls 呼び出しの前に、デバイスのグローバル ロックの取得、したがってミニポートがする必要がありますこの呼び出しをできるだけ高速実行します。 Portcls が (保留) をブロックする停止は保留中ですが、いずれかの新しい要求を作成します。 PortCls 再起動の保留は保留中の停止がキャンセルされたときに要求を作成します。

     

-   [**IAdapterPnpManagement::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604854) Ioctl のすべての操作を停止してから、アクティブなストリームを移動した後、Portcls によって呼び出される\[実行 | 一時停止 | 取得\]状態、\[停止\]状態。 この呼び出しは、デバイスのグローバル ロックを保持しているときに作成されません。 このため、ミニポートは、非同期操作 (作業項目、dpc、非同期スレッド) を待ち、そのオーディオ サブデバイスの登録を解除することです。 この呼び出しから戻る前に、ミニポートは必ず h または w のすべてのリソースがリリースされたことを確認する必要があります。

    **注**  ミニポートする必要がありますが明確でない場合、既存のオーディオ クライアントは、現在のハンドルを解放するため、削除する現在のミニポート/ストリーム オブジェクトを待ちません。 つまり、システムをクラッシュせず PnpStop スレッドが永久にブロックできません、PnP/電源スレッドです。

     

## <a name="span-idiminiportpnpnotifyspanspan-idiminiportpnpnotifyspanspan-idiminiportpnpnotifyspan-iminiportpnpnotify"></a><span id="_IMiniportPnpNotify"></span><span id="_iminiportpnpnotify"></span><span id="_IMINIPORTPNPNOTIFY"></span> IMiniportPnpNotify


[IMiniportPnpNotify](https://msdn.microsoft.com/library/windows/hardware/mt604855) PnP の状態を受信するミニポート オブジェクト (オーディオ サブデバイス) 変更通知を許可するオプションのインターフェイスします。

ミニポート PnP 停止の通知を受信各オーディオ サブデバイス登録した機会があります。 この通知を受信する、サブデバイスをサポートする必要があります[IMiniportPnpNotify](https://msdn.microsoft.com/library/windows/hardware/mt604855)します。 のみ、 [ **IMiniportPnpNotify::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604856)通知がこのインターフェイスで定義されています。

IMiniportPnpNotify インターフェイスの使用可能なは WaveRT およびトポロジの両方です。

**注**  のため Portcls 呼び出しの前にデバイスのグローバル ロックの取得、ミニポートでは、この呼び出しをできるだけ高速実行する必要があります。 ミニポートは、その他のスレッド/作業項目がデバイスのグローバル ロックを待機しているときにデッドロックを防止するには、この呼び出しの処理中に他のアクティビティを待ちませんする必要があります。 ミニポートが内で待機できる、必要な場合、 [ **IAdapterPnpManagement::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604854)呼び出します。

 

 

 




