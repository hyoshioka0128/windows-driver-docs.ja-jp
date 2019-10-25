---
title: オペレーティング システムによる PortCls のサポート
description: オペレーティング システムによる PortCls のサポート
ms.assetid: 87291410-41fa-49d2-a1e2-6d5d9b90deaf
keywords:
- オーディオミニポートドライバー WDK、ポートクラス
- ミニポートドライバー WDK オーディオ、ポートクラス
- ポートクラスライブラリ WDK オーディオ
- PortCls WDK audio, オペレーティングシステムごとのサポート
- オーディオ電源管理インターフェイス WDK
- オーディオストリームオブジェクトインターフェイス WDK
- オーディオミニポート補助インターフェイス WDK
- オーディオミニポートオブジェクトインターフェイス WDK
- オーディオポートオブジェクトインターフェイス WDK
- オーディオヘルパーオブジェクトインターフェイス WDK
- オーディオポートクラスインターフェイス WDK
- インターフェイス WDK ポートクラス
- プリフェッチオフセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c7a77748e929f2036f638e360deeff95846b99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832447"
---
# <a name="portcls-support-by-operating-system"></a>オペレーティング システムによる PortCls のサポート


## <span id="portcls_support_by_operating_system"></span><span id="PORTCLS_SUPPORT_BY_OPERATING_SYSTEM"></span>


次の一覧には、PortCls システムドライバー (Portcls) でサポートされているすべての関数とインターフェイスが含まれています。 リスト項目の前にアスタリスク (\*) が付いている場合、PortCls はその項目を Windows XP 以降でのみサポートします。 リスト項目の前に2つのアスタリスク (\*\*) がある場合、PortCls はその項目を Windows Vista 以降でのみサポートします。 その他のすべてのリスト項目は、すべてのバージョンの PortCls (Windows 2000 以降、Windows Me/98) でサポートされています。

### <a name="span-idaudio_port_class_functionsspanspan-idaudio_port_class_functionsspanspan-idaudio_port_class_functionsspanaudio-port-class-functions"></a><span id="Audio_Port_Class_Functions"></span><span id="audio_port_class_functions"></span><span id="AUDIO_PORT_CLASS_FUNCTIONS"></span>オーディオポートクラス関数

[**PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)

\* [ **PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCompleteIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompleteirp)

[**PcCompletePendingPropertyRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)

\* [ **PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccreatecontentmixed)

[ **Pcdestroycontent**の \*](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdestroycontent)

[**PcDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp)

\* [ **PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttodeviceobject)

\* [ **Pcforwardcontenttofileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttofileobject)

\* [ **Pcforwardcontenttointerface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcForwardIrpSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardirpsynchronous)

\* [ **Pcgetcontentrights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetcontentrights)

[**PcGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty)

[**PcGetTimeInterval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval)

[**PcInitializeAdapterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)

[**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)

[**PcNewInterruptSync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewinterruptsync)

[**PcNewMiniport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)

[**PcNewPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)

[**PcNewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewregistrykey)

[**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)

[**PcNewServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)

[**PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)

[**PcRegisterIoTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteriotimeout)

[**Pcregiphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)

[**外部への物理接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)

[**外部の物理 Connectiontoexternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)

[**Pcregisubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)

[**PcRequestNewPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcrequestnewpowerstate)

[**PcUnregisterIoTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteriotimeout)

### <a name="span-idaudio_helper_object_interfacesspanspan-idaudio_helper_object_interfacesspanspan-idaudio_helper_object_interfacesspanaudio-helper-object-interfaces"></a><span id="Audio_Helper_Object_Interfaces"></span><span id="audio_helper_object_interfaces"></span><span id="AUDIO_HELPER_OBJECT_INTERFACES"></span>オーディオヘルパーオブジェクトインターフェイス

[IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)

[IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)

\* [Idrmport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)

\* [IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)

[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

[Iportclsversion](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion)の \*

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

\* [Iprefetchoffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)

[Iサービスインク](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)

\*\* [Iunregisterphysicalconnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)

\*\* [Iunregistersubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)

### <a name="span-idaudio_port_object_interfacesspanspan-idaudio_port_object_interfacesspanspan-idaudio_port_object_interfacesspanaudio-port-object-interfaces"></a><span id="Audio_Port_Object_Interfaces"></span><span id="audio_port_object_interfaces"></span><span id="AUDIO_PORT_OBJECT_INTERFACES"></span>オーディオポートオブジェクトインターフェイス

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

\*\* [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

### <a name="span-idaudio_miniport_object_interfacesspanspan-idaudio_miniport_object_interfacesspanspan-idaudio_miniport_object_interfacesspanaudio-miniport-object-interfaces"></a><span id="Audio_Miniport_Object_Interfaces"></span><span id="audio_miniport_object_interfaces"></span><span id="AUDIO_MINIPORT_OBJECT_INTERFACES"></span>オーディオミニポートオブジェクトインターフェイス

[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)

\*\* [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)

### <a name="span-idaudio_miniport_auxiliary_interfacesspanspan-idaudio_miniport_auxiliary_interfacesspanspan-idaudio_miniport_auxiliary_interfacesspanaudio-miniport-auxiliary-interfaces"></a><span id="Audio_Miniport_Auxiliary_Interfaces"></span><span id="audio_miniport_auxiliary_interfaces"></span><span id="AUDIO_MINIPORT_AUXILIARY_INTERFACES"></span>オーディオミニポート補助インターフェイス

\* [Imusictechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology)

\* [Ipincount](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount)

### <a name="span-idaudio_stream_object_interfacesspanspan-idaudio_stream_object_interfacesspanspan-idaudio_stream_object_interfacesspanaudio-stream-object-interfaces"></a><span id="Audio_Stream_Object_Interfaces"></span><span id="audio_stream_object_interfaces"></span><span id="AUDIO_STREAM_OBJECT_INTERFACES"></span>オーディオストリームオブジェクトインターフェイス

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

\* [IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)

\*\* [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)

\*\* [Iportwavertstream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavertstream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

### <a name="span-idaudio_power_management_interfacesspanspan-idaudio_power_management_interfacesspanspan-idaudio_power_management_interfacesspanaudio-power-management-interfaces"></a><span id="Audio_Power_Management_Interfaces"></span><span id="audio_power_management_interfaces"></span><span id="AUDIO_POWER_MANAGEMENT_INTERFACES"></span>オーディオ電源管理インターフェイス

[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)

[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)

 

 




