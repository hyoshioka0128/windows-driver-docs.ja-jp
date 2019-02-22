---
title: 共有 PortCls プライベート PEP コンテキスト
description: Windows 8 以降、ミニポート ドライバーは Windows Power エンジン プラグイン (PEP) での共有秘密のコンテキストの IPortClsRuntimePower の新しいインターフェイスを使用できます。
ms.assetid: 27A0DD72-8AD0-4F38-B17C-9BDD63C5E7E1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6770297adafe12a4cb6d01637c2766c232039e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556887"
---
# <a name="portcls-private-pep-context-sharing"></a>共有 PortCls プライベート PEP コンテキスト


Windows 8 以降、ミニポート ドライバーは Windows Power エンジン プラグイン (PEP) での共有秘密のコンテキストの IPortClsRuntimePower の新しいインターフェイスを使用できます。

WaveRT ポートでの IPortClsRuntimePower の新しいインターフェイスを公開するオーディオ ポート クラス ドライバー (PortCls) が更新されました。 ミニポート ドライバー、オペレーティング システムの PEP にプライベートの電源制御を送信するためには、ミニポート ドライバーは、まず、関連付けられたポートの IPortClsRuntimePower インターフェイスにアクセスするがします。 ミニポート ドライバーは、プライベートの電源制御を送信するミニポート ドライバーを許可する適切な時に、呼び出されるコールバックを登録します。

## <a name="span-idaccessingiportclsruntimepowerspanspan-idaccessingiportclsruntimepowerspanspan-idaccessingiportclsruntimepowerspanaccessing-iportclsruntimepower"></a><span id="Accessing_IPortClsRuntimePower"></span><span id="accessing_iportclsruntimepower"></span><span id="ACCESSING_IPORTCLSRUNTIMEPOWER"></span>IPortClsRuntimePower へのアクセス


ミニポート ドライバーでは、次の一連のイベントを使用してそのポートの IPortClsRuntimePower にアクセスします。

1. ミニポート ドライバー呼び出し[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715) IID を提供および\_IPortWaveRT、REFID として。

2. **PcNewPort**型のポート インターフェイス (サポート) を作成します。 [IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)します。

3. ミニポート ドライバーで、新しく作成した QueryInterface を呼び出して**IPortWaveRT**インターフェイス、ポートし、IID を指定します\_IPortClsRuntimePower インターフェイスの GUID として。

4. **IPortWaveRT**ポート インターフェイスへのポインターをミニポート ドライバーを提供します。 その[ **IPortClsRuntimePower** ](https://msdn.microsoft.com/library/windows/hardware/dn265125)インターフェイス。

*Portcls.h*ヘッダー ファイルの GUID から、IPortClsRuntimePower 用の次のように定義します。

``` syntax
// {E057C351-0430-4DBC-B172-C711D40A2373}
DEFINE_GUID(IID_IPortClsRuntimePower,
0xe057c351, 0x430, 0x4dbc, 0xb1, 0x72, 0xc7, 0x11, 0xd4, 0xa, 0x23, 0x73);
```

## <a name="span-idregisteringacallbackspanspan-idregisteringacallbackspanspan-idregisteringacallbackspanregistering-a-callback"></a><span id="Registering_a_callback"></span><span id="registering_a_callback"></span><span id="REGISTERING_A_CALLBACK"></span>コールバックの登録


ミニポート ドライバーを使用して、 [ **IPortClsRuntimePower::RegisterPowerControlCallback** ](https://msdn.microsoft.com/library/windows/hardware/dn265126)コールバックを登録するメソッド。 PEP は、プライベートの要求を開始したときにまたはプライベートのミニポート ドライバー自体が開始した要求に対する応答では、このメソッドが呼び出されます。 コールバックの登録は、ドライバーは IRP を処理している間に通常実行する必要があります\_MN\_開始\_PNP Irp のデバイス。

コールバックで指定されているコンテキストのポインターとは別に、他のパラメーターは、ランタイム power framework の PowerControlCallback の定義を同じ定義されます。 さらに、ミニポートのコールバック型でなければなりません PCPFNRUNTIME\_POWER\_コントロール\_コールバックから次のスニペットで定義されている、 *Portcls.h*ヘッダー ファイル。

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

これを使用する必要があります、ドライバーを停止または削除すると、ときに、 [ **IPortClsRuntimePower::UnregisterPowerControlCallback** ](https://msdn.microsoft.com/library/windows/hardware/dn265128)いずれかの登録を解除するメソッドがコールバックを登録します。

## <a name="span-idsendingprivatepowercontrolsspanspan-idsendingprivatepowercontrolsspanspan-idsendingprivatepowercontrolsspansending-private-power-controls"></a><span id="Sending_private_power_controls"></span><span id="sending_private_power_controls"></span><span id="SENDING_PRIVATE_POWER_CONTROLS"></span>送信側のプライベート power コントロール


ミニポートへのアクセスを確立した後で、 **IPortClsRuntimePower**インターフェイス、およびインターフェイスの使用**RegisterPowerControlCallback**コールバックを登録するメソッドをプライベートに送信する準備がようになりました電源を制御します。 ミニポート ドライバーを使用して、コールバック メソッドが呼び出されたときに、 [ **IPortClsRuntimePower::SendPowerControl** ](https://msdn.microsoft.com/library/windows/hardware/dn265127) Windows PEP にプライベートの電源制御を送信する方法。

例外として、*デバイス オブジェクト*パラメーター、その他のすべてのパラメーターがのランタイム power framework の場合と同じで定義されている[PoFxPowerControl](https://msdn.microsoft.com/library/windows/hardware/hh439518.aspx)メソッド。

 

 




