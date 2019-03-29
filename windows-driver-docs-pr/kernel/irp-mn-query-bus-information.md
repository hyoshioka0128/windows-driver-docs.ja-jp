---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP マネージャーでは、この IRP を使用して、デバイスの親のバスの種類とインスタンスの数を要求します。バス ドライバーには、子デバイス (Pdo) は、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: ecc14699760e5904e484a58d5f7f128f105d7ed9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573355"
---
# <a name="irpmnquerybusinformation"></a>IRP\_MN\_クエリ\_BUS\_情報


PnP マネージャーでは、この IRP を使用して、デバイスの親のバスの種類とインスタンスの数を要求します。

バス ドライバーには、子デバイス (Pdo) は、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスが列挙されたときに、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**完成したへのポインターに[ **PNP\_BUS\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff559608)構造体。 (詳細については「操作」セクションを参照してください)。バス ドライバーの設定エラーが発生、 **Irp -&gt;IoStatus.Information**をゼロにします。

関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="operation"></a>操作
---------

この IRP への応答で返される情報は、関数とフィルター ドライバー、バス上のデバイス用に提供されます。 関数とフィルター ドライバーが呼び出せる[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)要求に、 **DevicePropertyBusTypeGuid**、 **DevicePropertyLegacyBusType**、または**DevicePropertyBusNumber**します。 1 つ以上のバス上のデバイスをサポートする関数とフィルター ドライバーは、この情報を使用するバスの特定のデバイスが存在するかを判断します。

割り当てるバス ドライバーでは、この IRP への応答の情報が返された場合、 **PNP\_バス\_情報**ページングされたメモリから構造体。 PnP マネージャーは、不要になったときに、構造体を解放します。

A **PNP\_BUS\_情報**構造体には、次の形式。

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

構造体のメンバーの定義は次のとおりです。

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
バス ドライバー設定**BusTypeGuid**デバイスが存在するバスの種類の guid。 Wdmguid.h 標準バスの種類の Guid が表示されます。 ドライバー開発者は、Uuidgen を使用して他のバスの種類の Guid を生成する必要があります。

<a href="" id="legacybustype"></a>**LegacyBusType**  
PnP バス ドライバー設定**LegacyBusType**を[**インターフェイス\_型**](https://msdn.microsoft.com/library/windows/hardware/ff547839)親バスの。 インターフェイスの種類は、Wdm.h で定義されます。 いくつかのバスがある特定の**インターフェイス\_型**などの値**PCMCIABus**、 **PCIBus**、または**PNPISABus**します。 他のバスでは、特に新しいバスなどの USB、バス ドライバーでは、このメンバーを設定**PNPBus**します。

**LegacyBusType**デバイスと通信するために使用するインターフェイスを指定します。 これは、親のバスの種類に対応していない可能性があります。 たとえば、PCI CardBus コント ローラーに接続されている CardBus カード用のインターフェイスは**PCIBus**します。 ただし、PCI CardBus コント ローラーに PCMCIA カードのインターフェイスは**PCMCIABus**します。

<a href="" id="busnumber"></a>**BusNumber**  
バス ドライバー設定**BusNumber**他のコンピューター上の同じ種類のバスのバスの識別番号。 バス番号付けスキームは、bus 固有です。 バス番号は、仮想、可能性がありますなどの従来のインターフェイスで使用される番号と一致する必要があります[ **IoReportResourceUsage**](https://msdn.microsoft.com/library/windows/hardware/ff549616)します。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

呼び出す[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)デバイスが接続されているバスに関する情報を取得します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)

 

 




