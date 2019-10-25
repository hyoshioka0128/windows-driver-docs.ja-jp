---
title: オーディオ ポート クラスの関数
description: オーディオ ポート クラスの関数
ms.assetid: dc8f32e8-b01c-4f06-a32f-c08f76001f79
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3086bdd66d779e76fddae199f9166612f5d2e2c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833661"
---
# <a name="audio-port-class-functions"></a>オーディオ ポート クラスの関数


## <span id="ddk_audio_port_class_functions_ks"></span><span id="DDK_AUDIO_PORT_CLASS_FUNCTIONS_KS"></span>


このセクションでは、PortCls システムドライバー (PortCls) によって提供される一般的な関数について、アルファベット順に説明します。 これらの関数は、どのインターフェイスにも属していません。 これらは、PortCls への登録やサブデバイスのインストールなど、一般的なユーティリティの操作を実行するためにオーディオミニポートドライバーによって使用されます。

さまざまな PortCls 機能をサポートするオペレーティングシステムのバージョンの一覧については、「 [PortCls support By オペレーティング system](https://docs.microsoft.com/windows-hardware/drivers/audio/portcls-support-by-operating-system)」を参照してください。

PortCls は、次の関数を実装します。

[**PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)

[**PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCompleteIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompleteirp)

[**PcCompletePendingPropertyRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)

[**PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccreatecontentmixed)

[**PcDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdestroycontent)

[**PcDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp)

[**PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttodeviceobject)

[**PcForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttofileobject)

[**PcForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcForwardIrpSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardirpsynchronous)

[**PcGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetcontentrights)

[**PcGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty)

[**PcGetPhysicalDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetphysicaldeviceobject)

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

[**PcUnregisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)

[**PcUnregisterIoTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteriotimeout)

 

 





