---
title: PortCls プライベート PEP コンテキストの共有
description: Windows 8 以降では、ミニポートドライバーは IPortClsRuntimePower (新しいインターフェイス) を使用して、Windows パワーエンジンプラグイン (PEP) とのプライベートコンテキスト共有を行うことができます。
ms.assetid: 27A0DD72-8AD0-4F38-B17C-9BDD63C5E7E1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1d367a896af137df61f43b0b1fd09d37941a4b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832465"
---
# <a name="portcls-private-pep-context-sharing"></a>PortCls プライベート PEP コンテキストの共有


Windows 8 以降では、ミニポートドライバーは IPortClsRuntimePower (新しいインターフェイス) を使用して、Windows パワーエンジンプラグイン (PEP) とのプライベートコンテキスト共有を行うことができます。

オーディオポートクラスドライバー (PortCls) が更新され、WaveRT ポートで新しいインターフェイス IPortClsRuntimePower が公開されました。 ミニポートドライバーからオペレーティングシステムの PEP にプライベート電源管理を送信するには、まず、関連付けられているポートの IPortClsRuntimePower インターフェイスにミニポートドライバーがアクセスする必要があります。 ミニポートドライバーは、適切なタイミングで呼び出されるコールバックを登録し、ミニポートドライバーがプライベート電源コントロールを送信できるようにします。

## <a name="span-idaccessing_iportclsruntimepowerspanspan-idaccessing_iportclsruntimepowerspanspan-idaccessing_iportclsruntimepowerspanaccessing-iportclsruntimepower"></a><span id="Accessing_IPortClsRuntimePower"></span><span id="accessing_iportclsruntimepower"></span><span id="ACCESSING_IPORTCLSRUNTIMEPOWER"></span>IPortClsRuntimePower へのアクセス


ミニポートドライバーは、次の一連のイベントを使用して、ポートの IPortClsRuntimePower へのアクセスを取得します。

1. ミニポートドライバーは[**Pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出し、IID\_IPORTWAVERT を REFID として提供します。

2. **Pcnewport**は、 [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)型のポートインターフェイス (pport) を作成します。

3. 次に、ミニポートドライバーは、新しく作成された**IPortWaveRT** port インターフェイスで QueryInterface を呼び出し、インターフェイス GUID として\_IPortClsRuntimePower という IID を指定します。

4. **IPortWaveRT** port インターフェイスは、ミニポートドライバーに[**Iportclsruntimepower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsruntimepower) interface へのポインターを提供します。

Portcls ヘッダーファイルは、次のように IPortClsRuntimePower の GUID を定義し*ます。*

``` syntax
// {E057C351-0430-4DBC-B172-C711D40A2373}
DEFINE_GUID(IID_IPortClsRuntimePower,
0xe057c351, 0x430, 0x4dbc, 0xb1, 0x72, 0xc7, 0x11, 0xd4, 0xa, 0x23, 0x73);
```

## <a name="span-idregistering_a_callbackspanspan-idregistering_a_callbackspanspan-idregistering_a_callbackspanregistering-a-callback"></a><span id="Registering_a_callback"></span><span id="registering_a_callback"></span><span id="REGISTERING_A_CALLBACK"></span>コールバックの登録


ミニポートドライバーは、 [**Iportclsruntimepower:: RegisterPowerControlCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-registerpowercontrolcallback)メソッドを使用して、コールバックを登録します。 このメソッドは、PEP がプライベート要求を開始したとき、またはミニポートドライバー自体によって開始されたプライベート要求への応答として呼び出されます。 通常、コールバックの登録は、ドライバーが IRP\_を処理している間に実行し、\_デバイスの PNP Irp を開始\_ます。

コールバックで指定されたコンテキストポインターとは別に、その他のパラメーターは、ランタイム電源フレームワークの PowerControlCallback の定義と同じように定義されます。 さらに、ミニポートのコールバックは、 *Portcls*ヘッダーファイルの次のスニペットで定義されているように、PCPFNRUNTIME\_POWER\_CONTROL\_callback 型である必要があります。

```ManagedCPlusPlus
typedef
NTSTATUS
_IRQL_requires_max_(DISPATCH_LEVEL)
(*PCPFNRUNTIME_POWER_CONTROL_CALLBACK)
(
    _In_        LPCGUID PowerControlCode,
    _In_opt_    PVOID   InBuffer,
    _In_        SIZE_T  InBufferSize,
    _Out_opt_   PVOID   OutBuffer,
    _In_        SIZE_T  OutBufferSize,
    _Out_opt_   PSIZE_T BytesReturned,
    _In_opt_    PVOID   Context
);
```

ドライバーが停止または削除された場合、登録されているコールバックの登録を解除するには、 [**Iportclsruntimepower:: UnregisterPowerControlCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-unregisterpowercontrolcallback)メソッドを使用する必要があります。

## <a name="span-idsending_private_power_controlsspanspan-idsending_private_power_controlsspanspan-idsending_private_power_controlsspansending-private-power-controls"></a><span id="Sending_private_power_controls"></span><span id="sending_private_power_controls"></span><span id="SENDING_PRIVATE_POWER_CONTROLS"></span>プライベート電源管理の送信


ミニポートが**Iportclsruntimepower**インターフェイスへのアクセスを確立し、インターフェイスの**registerpowercontrolcallback**メソッドを使用してコールバックを登録すると、プライベート電源コントロールを送信する準備が整いました。 コールバックメソッドが呼び出されると、ミニポートドライバーは[**Iportclsruntimepower:: SendPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-sendpowercontrol)メソッドを使用して、プライベート電源管理を Windows PEP に送信します。

*DeviceObject*パラメーターを除き、他のすべてのパラメーターは、ランタイムの power Framework の[Pofxpowercontrol](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)メソッドと同じように定義されています。

 

 




