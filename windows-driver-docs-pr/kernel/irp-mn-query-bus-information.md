---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP マネージャーは、この IRP を使用して、デバイスの親バスの種類とインスタンス番号を要求します。バスドライバーは、子デバイス (PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: d46b41d07a6cd4408c505824251e1136bf494d1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828032"
---
# <a name="irp_mn_query_bus_information"></a>IRP\_\_クエリ\_バス\_情報


PnP マネージャーは、この IRP を使用して、デバイスの親バスの種類とインスタンス番号を要求します。

バスドライバーは、子デバイス (PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスが列挙されたときにこの IRP を送信します。

PnP マネージャーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

正常に実行された場合、バスドライバーは**Irp&gt;IoStatus. 情報**を、完了した[**PNP\_バス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)構造体へのポインターに設定します。 (詳細については、「操作」セクションを参照してください)。エラーが発生した場合、バスドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。

<a name="operation"></a>操作
---------

この IRP への応答として返される情報は、バス上のデバイスの関数とフィルタードライバーで使用できます。 関数とフィルタードライバーは[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、 **Devicepropertybustypeguid**、 **DevicePropertyLegacyBusType**、または**devicepropertybusnumber**を要求できます。 複数のバス上のデバイスをサポートする関数とフィルタードライバーは、この情報を使用して、特定のデバイスがどのバスに存在するかを判断できます。

バスドライバーは、この IRP に応答して情報を返す場合、ページングされたメモリから、 **PNP\_bus\_情報**構造体を割り当てます。 不要になったときに、PnP マネージャーによって構造が解放されます。

**PNP\_BUS\_情報**構造体の形式は次のとおりです。

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

構造体のメンバーは、次のように定義されます。

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
バスドライバーは、デバイスが存在するバスの種類の GUID に**Bustypeguid**を設定します。 標準バスタイプの Guid は、Wdmguid. h に記載されています。 ドライバーの作成者は、Uuidgen.exe を使用して他の種類のバスの Guid を生成する必要があります。

<a href="" id="legacybustype"></a>**LegacyBusType**  
PnP バスドライバーは、 **LegacyBusType**を、親バスの[ **\_型のインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type)に設定します。 インターフェイスの種類は、Wdm で定義されています。 一部のバスには、 **PCMCIABus**、 **PCIBus**、 **PNPISABus**など、特定の**インターフェイス\_型**の値があります。 他のバス、特に新しいバス (USB など) の場合、バスドライバーはこのメンバーを**PNPBus**に設定します。

**LegacyBusType**は、デバイスとの通信に使用するインターフェイスを指定します。 これは、親バスの種類に対応している場合もあれば、対応していない場合もあります。 たとえば、PCI CardBus コントローラーに接続されている CardBus カードのインターフェイスは、 **PCIBus**です。 ただし、PCI CardBus コントローラー上の PCMCIA カードのインターフェイスは**PCMCIABus**です。

<a href="" id="busnumber"></a>**BusNumber**  
バスドライバーは、 **Busnumber**を、コンピューター上の同じ種類の他のバスと区別する数値に設定します。 バス番号付けスキームはバス固有です。 バス番号は仮想にすることができますが、 [**IoReportResourceUsage**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)などの従来のインターフェイスで使用されている番号と一致する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、デバイスが接続されているバスに関する情報を取得します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




