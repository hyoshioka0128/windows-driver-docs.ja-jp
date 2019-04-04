---
title: オーディオ ポート クラス関数
description: オーディオ ポート クラス関数
ms.assetid: dc8f32e8-b01c-4f06-a32f-c08f76001f79
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 899fe1a89ca73f578b184892219020c68f99fd9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532141"
---
# <a name="audio-port-class-functions"></a>オーディオ ポート クラス関数


## <span id="ddk_audio_port_class_functions_ks"></span><span id="DDK_AUDIO_PORT_CLASS_FUNCTIONS_KS"></span>


このセクションには、PortCls システム ドライバー (portcls.sys) を提供する一般的な機能がアルファベットの順に説明します。 これらの関数は、任意のインターフェイスには属していません。 一般的なユーティリティ、PortCls を登録し、サブデバイスをインストールするなどの操作を実行するオーディオ ミニポート ドライバーによって使用されます。

さまざまな PortCls 関数をサポートしているバージョンのオペレーティング システムの一覧は、[オペレーティング システムによって PortCls サポート](https://msdn.microsoft.com/library/windows/hardware/ff537762)を参照してください。

PortCls には、次の関数が実装されています。

[**PcAddAdapterDevice**](https://msdn.microsoft.com/library/windows/hardware/ff537683)

[**PcAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff537684)

[**PcCompleteIrp**](https://msdn.microsoft.com/library/windows/hardware/ff537686)

[**PcCompletePendingPropertyRequest**](https://msdn.microsoft.com/library/windows/hardware/ff537687)

[**PcCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff537689)

[**PcDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff537690)

[**PcDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/ff537691)

[**PcForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff537696)

[**PcForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff537697)

[**PcForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff537698)

[**PcForwardIrpSynchronous**](https://msdn.microsoft.com/library/windows/hardware/ff537699)

[**PcGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff537700)

[**PcGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff537701)

[**PcGetPhysicalDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/hh706182)

[**PcGetTimeInterval**](https://msdn.microsoft.com/library/windows/hardware/ff537702)

[**PcInitializeAdapterDriver**](https://msdn.microsoft.com/library/windows/hardware/ff537703)

[**PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)

[**PcNewInterruptSync**](https://msdn.microsoft.com/library/windows/hardware/ff537713)

[**PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)

[**PcNewPort**](https://msdn.microsoft.com/library/windows/hardware/ff537715)

[**PcNewRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff537716)

[**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)

[**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)

[**PcNewServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff537719)

[**PcRegisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537724)

[**PcRegisterIoTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff537725)

[**PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)

[**PcRegisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537728)

[**PcRegisterPhysicalConnectionToExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537729)

[**PcRegisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537731)

[**PcRequestNewPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff537733)

[**PcUnregisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537735)

[**PcUnregisterIoTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff537736)

 

 





