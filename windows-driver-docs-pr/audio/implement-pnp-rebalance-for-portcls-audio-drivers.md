---
title: PortCls オーディオ ドライバー用に PnP 再調整を実装する
description: PnP の再調整は、メモリリソースを再割り当てする必要がある特定の PCI シナリオで使用されます。
ms.assetid: FCAD7F8B-AA9B-430A-BCAF-04E13FA15382
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 09127584c88810af766c0b36c5910e45c10a1def
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833269"
---
# <a name="implement-pnp-rebalance-for-portcls-audio-drivers"></a>PortCls オーディオ ドライバー用に PnP 再調整を実装する


PnP の再調整は、メモリリソースを再割り当てする必要がある特定の PCI シナリオで使用されます。

再調整は、主に次の2つのシナリオで発生します。

1. PCI hotplug: ユーザーがデバイスに接続し、PCI バスに新しいデバイス用のドライバーを読み込むための十分なリソースがありません。 このカテゴリに分類されるデバイスの例として、Thunderbolt icon、USB-C、および NVME ストレージがあります。 このシナリオでは、追加する追加のデバイスをサポートするために、メモリリソースを再編成して統合する必要があります (再分配)。
2. PCI 再測定可能なバー: デバイスのドライバーがメモリに正常に読み込まれた後、追加のリソースを要求します。 デバイスの例としては、ハイエンドグラフィックスカードや記憶装置などがあります。 ビデオドライバーサポートの詳細については、「[サイズ変更](https://docs.microsoft.com/windows-hardware/drivers/display/resizable-bar-support)可能なバーのサポート」を参照してください。
このトピックでは、PortCls オーディオドライバーの PnP 再調整を実装するために必要な作業について説明します。

PnP の再調整は、Windows 10 バージョン1511以降のバージョンの Windows で使用できます。

## <a name="span-idrebalance_requirementsspanspan-idrebalance_requirementsspanspan-idrebalance_requirementsspanrebalance-requirements"></a><span id="Rebalance_Requirements"></span><span id="rebalance_requirements"></span><span id="REBALANCE_REQUIREMENTS"></span>再調整要件


Portcls オーディオドライバーには、次の条件が満たされた場合に再調整をサポートする機能があります。

-   ミニポートは、 [IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement)インターフェイスを Portcls に登録する必要があります。
-   ミニポートは、 [**IAdapterPnpManagement:: GetSupportedRebalanceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-getsupportedrebalancetype)から PcRebalanceRemoveSubdevices を返す必要があります。
-   トポロジと WaveRT は、2つのポートの種類をサポートしています。

アクティブなオーディオストリームがあるときの再調整をサポートするために、portcls オーディオドライバーは、次の2つの追加要件のいずれかを満たす必要があります。

-   ドライバーは、オーディオストリームの[**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)および[IMiniportWaveRTOutputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertoutputstream)パケットインターフェイスをサポートしています。 このオプションを選択することをお勧めします。

または

-   ドライバーがストリームの get/write IMiniportWaveRT をサポートしていない場合、ドライバーは[**Ksk プロパティ\_rtaudio\_positionregister**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-rtaudio-positionregister)および[**KSK プロパティ\_RTAUDIO\_clockregister**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-rtaudio-clockregister)をサポートしていない必要があります。 オーディオエンジンは、このシナリオで[**IMiniportWaveRTStream:: GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))を使用します。

## <a name="span-idaudio_stream_behavior_when_rebalancing_occursspanspan-idaudio_stream_behavior_when_rebalancing_occursspanspan-idaudio_stream_behavior_when_rebalancing_occursspanaudio-stream-behavior-when-rebalancing-occurs"></a><span id="Audio_Stream_Behavior_When_Rebalancing_Occurs"></span><span id="audio_stream_behavior_when_rebalancing_occurs"></span><span id="AUDIO_STREAM_BEHAVIOR_WHEN_REBALANCING_OCCURS"></span>再調整が発生したときのオーディオストリームの動作


再調整がトリガーされ、アクティブなオーディオストリームがある場合、およびドライバーがアクティブなオーディオストリームの再調整をサポートしている場合、アクティブなオーディオストリームはすべて停止され、自動的に再起動されません。

## <a name="span-idiportclspnp_com_interfacespanspan-idiportclspnp_com_interfacespanspan-idiportclspnp_com_interfacespaniportclspnp-com-interface"></a><span id="IPortClsPnp_COM_Interface"></span><span id="iportclspnp_com_interface"></span><span id="IPORTCLSPNP_COM_INTERFACE"></span>IPortClsPnp COM インターフェイス


`IPortClsPnp` は、ポートクラスドライバー (PortCls) がアダプターに公開する PnP 管理インターフェイスです。

`IPortClsPnp` は**IUnknown**から継承され、次のメソッドもサポートしています。

-   [**IPortClsPnp:: RegisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-registeradapterpnpmanagement)
-   [**IPortClsPnp:: UnregisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-unregisteradapterpnpmanagement)

オーディオミニポートドライバーは、Portcls エクスポートを使用して、または WaveRT ポートオブジェクトで公開されている[**iportclspnp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspnp) COM インターフェイス iportclspnp 経由で、PNP 通知インターフェイスを登録できます。 [**Iportclspnp:: RegisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-registeradapterpnpmanagement)と[**Iportclspnp:: UnregisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-unregisteradapterpnpmanagement)を使用して、登録と登録解除を行います。

## <a name="span-idrequired_portcls_export_ddisspanspan-idrequired_portcls_export_ddisspanspan-idrequired_portcls_export_ddisspanrequired-portcls-export-ddis"></a><span id="Required_PortCls_Export_DDIs"></span><span id="required_portcls_export_ddis"></span><span id="REQUIRED_PORTCLS_EXPORT_DDIS"></span>必須の PortCls Export DDIs


[IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement)は、PnP 管理メッセージを受信する必要がある場合に、アダプターが実装および登録する必要があるインターフェイスです。 [**PcRegisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpnpmanagement)を使用して、このインターフェイスを PortCls に登録します。 [**PcUnregisterAdapterPnpManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpnpmanagement)を使用して、このインターフェイスの登録を PortCls で解除します。

## <a name="span-idrequired_driver_ddisspanspan-idrequired_driver_ddisspanspan-idrequired_driver_ddisspanrequired-driver-ddis"></a><span id="Required_Driver_DDIs"></span><span id="required_driver_ddis"></span><span id="REQUIRED_DRIVER_DDIS"></span>必要なドライバーの DDIs


再調整をサポートするには、次の[IAdapterPnpManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) DDIs を実装する必要があります。

-   [**IAdapterPnpManagement:: GetSupportedRebalanceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-getsupportedrebalancetype)は、querystop の処理中に Portcls によって呼び出されます。 ミニポートは、PC で定義されている、サポートされている調整の種類を返します。 [ **\_\_種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-pc_rebalance_type)の列挙型を調整します。

    この呼び出しを行う前に、Portcls がデバイスのグローバルロックを取得する  **ことに注意**してください。したがって、ミニポートは、できるだけ高速にこの呼び出しを実行する必要があります。

     

-   [**IAdapterPnpManagement::P npquerystop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpquerystop)は、QUERYSTOP IRP の次の直後に portcls によって呼び出されます。 これは通知であり、呼び出しは値を返しません。

    この呼び出しを行う前に、Portcls がデバイスのグローバルロックを取得する  **ことに注意**してください。したがって、ミニポートは、できるだけ高速にこの呼び出しを実行する必要があります。 停止が保留中の場合、Portcls は新しい create 要求をブロック (保留) します。

     

-   [**IAdapterPnpManagement::P npcancelstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpcancelstop)は、CanceStop IRP の処理中に portcls によって呼び出されます。 これは通知だけです。 以前に PnpQueryStop 通知を受信しなくても、ミニポートは PnpCancelStop を受信する可能性があります。 この動作に対応するために、ミニポートを作成する必要があります。 たとえば、Portcls がこの通知をミニポートに転送する機会を得る前に、QueryStop ロジックが IRP に失敗した場合に発生します。 このシナリオでは、PnP マネージャーは引き続き PnP キャンセルの停止を呼び出します。

    この呼び出しを行う前に、Portcls がデバイスのグローバルロックを取得する  **ことに注意**してください。したがって、ミニポートは、できるだけ高速にこの呼び出しを実行する必要があります。 停止が保留中の場合、Portcls は新しい create 要求をブロック (保留) します。 保留の停止が取り消されると、PortCls は保留中の作成要求を再開します。

     

-   [**IAdapterPnpManagement::P npstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpstop)は、すべての Ioctl 操作を停止し、アクティブなストリームを \[run | pause |\] の状態を \[stop\] 状態に移動した後に、Portcls によって呼び出されます。 この呼び出しは、デバイスのグローバルロックを保持している間は行われません。 そのため、ミニポートは、非同期操作 (作業項目、dpc、非同期スレッド) を待機し、そのオーディオサブデバイスの登録を解除することができます。 この呼び出しから戻る前に、ミニポートですべての h/w リソースが解放されていることを確認する必要があります。

    既存のオーディオクライアントが現在のハンドルを解放するときに、ミニポートまたはストリームオブジェクトが削除されるのをミニポートで待機させることはできません  **注意**してください。 PnpStop スレッドは、システムをクラッシュさせずに永遠をブロックすることはできません。つまり、これは PnP/電源スレッドです。

     

## <a name="span-id_iminiportpnpnotifyspanspan-id_iminiportpnpnotifyspanspan-id_iminiportpnpnotifyspan-iminiportpnpnotify"></a><span id="_IMiniportPnpNotify"></span><span id="_iminiportpnpnotify"></span><span id="_IMINIPORTPNPNOTIFY"></span>IMiniportPnpNotify


[IMiniportPnpNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportpnpnotify)は、ミニポートオブジェクト (オーディオサブデバイス) が PnP 状態の変更通知を受信できるようにするための省略可能なインターフェイスです。

ミニポートは、登録されているオーディオサブデバイスごとに PnP 停止通知を受け取ることができます。 この通知を受信するには、サブデバイスが[IMiniportPnpNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportpnpnotify)をサポートしている必要があります。 このインターフェイスでは、 [**IMiniportPnpNotify::P npstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportpnpnotify-pnpstop) notification のみが定義されています。

IMiniportPnpNotify インターフェイスは、WaveRT とトポロジの両方で使用できます。

Portcls はこの呼び出しを行う前にデバイスのグローバルロックを取得するので、ミニポートはできるだけ高速にこの呼び出しを実行する必要があります **。  ** 他のスレッドまたは作業項目がデバイスのグローバルロックを待機しているときにデッドロックが発生しないようにするには、この呼び出しの処理中にミニポートで他のアクティビティを待機することはできません。 必要に応じて、ミニポートは[**IAdapterPnpManagement::P npstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpstop)呼び出しで待機できます。

