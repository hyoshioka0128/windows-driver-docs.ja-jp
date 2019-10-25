---
title: レジストリ キーのオブジェクト
description: レジストリ キーのオブジェクト
ms.assetid: c666f0cc-5a8a-4df8-9c65-08e3b044a08f
keywords:
- ヘルパーオブジェクト WDK オーディオ、レジストリキーオブジェクト
- レジストリキーオブジェクト WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcc9cc335f01795f22a5539d98f8b4cc16ee4dc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830224"
---
# <a name="registry-key-objects"></a>レジストリ キーのオブジェクト


## <span id="registry_key_objects"></span><span id="REGISTRY_KEY_OBJECTS"></span>


PortCls システムドライバーは、ミニポートドライバーの利点を得るために[Iregistrykey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)インターフェイスを実装しています。 IRegistryKey オブジェクトは、レジストリキーを表します。 ミニポートドライバーは、次の操作を行うためにレジストリキーオブジェクトを使用します。

-   レジストリキーの作成と削除

-   レジストリキーの列挙

-   クエリとレジストリキーの設定

指定されたキーの下にあるレジストリエントリに関する情報をレジストリキーオブジェクトに照会すると、クエリは3つの形式のいずれかで情報を出力することができ、それぞれが異なるキークエリ構造を使用します。 次の表に、クエリによって出力される3つのキークエリ構造の種類を示す、\_クラス列挙値の[**キー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_key_information_class)を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KEY_INFORMATION_CLASS 値</th>
<th align="left">キークエリの構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>KeyBasicInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_basic_information" data-raw-source="[&lt;strong&gt;KEY_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_basic_information)"><strong>KEY_BASIC_INFORMATION</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>キー・マトリックス</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_full_information" data-raw-source="[&lt;strong&gt;KEY_FULL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_full_information)"><strong>KEY_FULL_INFORMATION</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>KeyNodeInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_node_information" data-raw-source="[&lt;strong&gt;KEY_NODE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_key_node_information)"><strong>KEY_NODE_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

既存のレジストリキーを開くか、新しいレジストリキーを作成するには、アダプタードライバーが[**Pcnewregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewregistrykey)関数を呼び出すことができます。また、ミニポートドライバーは、ポートドライバーの[**IPort:: newregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-newregistrykey)メソッドを呼び出すことができます。 2つの呼び出しは似ていますが、 **Pcnewregistrykey**関数には、 *DeviceObject*と*subdevice*という2つの追加パラメーターが必要です。 詳細については、「 **Pcnewregistrykey**」を参照してください。

ミニポートドライバーによって新しい[Iregistrykey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)オブジェクトが作成されると、既存のサブキーが開かれるか、または新しいレジストリサブキーが存在しない場合は作成されます。 どちらの場合も、レジストリキーオブジェクトはキーへのハンドルを格納します。 このオブジェクトが後で解放され、その参照カウントが0に減少すると、オブジェクトはキーへのハンドルを自動的に閉じます。

[Iregistrykey](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)インターフェイスは、次のメソッドをサポートしています。

[**IRegistryKey::D eleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-deletekey)

[**IRegistryKey:: EnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-enumeratekey)

[**IRegistryKey:: EnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-enumeratevaluekey)

[**IRegistryKey:: NewSubKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-newsubkey)

[**IRegistryKey:: QueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-querykey)

[**IRegistryKey:: QueryRegistryValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-queryregistryvalues)

[**IRegistryKey:: QueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-queryvaluekey)

[**IRegistryKey:: SetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iregistrykey-setvaluekey)

 

 




