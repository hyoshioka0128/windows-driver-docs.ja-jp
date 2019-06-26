---
title: レジストリ キーのオブジェクト
description: レジストリ キーのオブジェクト
ms.assetid: c666f0cc-5a8a-4df8-9c65-08e3b044a08f
keywords:
- ヘルパーは、WDK オーディオ、レジストリ キー オブジェクトをオブジェクトします。
- レジストリ キー オブジェクトの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0c5a8bf902385b163568e8c35eece77fa41800c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355273"
---
# <a name="registry-key-objects"></a>レジストリ キーのオブジェクト


## <span id="registry_key_objects"></span><span id="REGISTRY_KEY_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)ミニポート ドライバーのためのインターフェイス。 IRegistryKey オブジェクトは、レジストリ キーを表します。 ミニポート ドライバーでは、レジストリ キー オブジェクトを使用して、次の操作します。

-   作成し、レジストリ キーの削除

-   レジストリ キーを列挙します。

-   クエリを実行し、レジストリ キーを設定

については、指定したキーの下のレジストリ エントリをレジストリ キー オブジェクトを照会するときに、クエリは異なるキー クエリ構造体を使用してそれぞれの 3 つの形式のいずれかの情報を出力できます。 次の表は、 [**キー\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_key_information_class)の 3 つのキー クエリの構造を示す列挙値は、クエリによって出力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KEY_INFORMATION_CLASS 値</th>
<th align="left">キー クエリ構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>KeyBasicInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_basic_information" data-raw-source="[&lt;strong&gt;KEY_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_basic_information)"><strong>KEY_BASIC_INFORMATION</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>KeyFullInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_full_information" data-raw-source="[&lt;strong&gt;KEY_FULL_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_full_information)"><strong>KEY_FULL_INFORMATION</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>KeyNodeInformation</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_node_information" data-raw-source="[&lt;strong&gt;KEY_NODE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_key_node_information)"><strong>KEY_NODE_INFORMATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

既存のレジストリ キーを開くか、新しいレジストリ キーの作成、アダプタのドライバを呼び出すことができます、 [ **PcNewRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewregistrykey)関数、およびミニポート ドライバーには、ポート ドライバーを呼び出すことができます[ **IPort::NewRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-newregistrykey)メソッド。 2 つの呼び出しは似ていますが、 **PcNewRegistryKey**関数には、2 つのパラメーターの追加が必要な*デバイス オブジェクト*と*サブデバイス*。 詳細については、次を参照してください。 **PcNewRegistryKey**します。

ミニポート ドライバーが新しいを作成します[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)オブジェクト、オブジェクトは、既存のサブキーを開きますかが存在しない場合は、新しいレジストリ サブキーを作成します。 どちらの場合は、レジストリ キー オブジェクトは、キーを識別するハンドルを格納します。 そのオブジェクトが後で解放されるときに、その参照カウントをデクリメントを 0 に、オブジェクトは、キーへのハンドルを自動的に閉じます。

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)インターフェイスは、次のメソッドをサポートしています。

[**IRegistryKey::DeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-deletekey)

[**IRegistryKey::EnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-enumeratekey)

[**IRegistryKey::EnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-enumeratevaluekey)

[**IRegistryKey::NewSubKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-newsubkey)

[**IRegistryKey::QueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-querykey)

[**IRegistryKey::QueryRegistryValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-queryregistryvalues)

[**IRegistryKey::QueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-queryvaluekey)

[**IRegistryKey::SetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iregistrykey-setvaluekey)

 

 




