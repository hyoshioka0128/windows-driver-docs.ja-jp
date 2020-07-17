---
title: DEVPKEY_Device_ContainerId
description: DEVPKEY_Device_ContainerId
ms.assetid: 9d5be913-b699-4d8f-aa3f-53ad5dbe6482
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_ContainerId
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ContainerId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f52406f42f44050afa4e1ee392ca3af29d07c70f
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418364"
---
# <a name="devpkey_device_containerid"></a>DEVPKEY_Device_ContainerId


DEVPKEY_Device_ContainerId デバイスプロパティは、1つまたは複数のデバイスノード (*devnodes*) を物理デバイスのインスタンスを表す*デバイスコンテナー*にグループ化するために、プラグアンドプレイ (PnP) マネージャーによって使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ContainerId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

Windows 7 以降では、PnP マネージャーはデバイスコンテナーとその識別子 (*ContainerID*) を使用して、特定の物理デバイスの各インスタンスに属している1つ以上の*devnodes*をグループ化します。 デバイスインスタンスの ContainerID は、DEVPKEY_Device_ContainerId デバイスプロパティを通じて参照されます。

1つのデバイスのインスタンスから生成されたすべての devnodes をコンテナーにグループ化すると、次の結果が得られます。

-   オペレーティングシステムは、物理デバイスから生成された*devnodes*間で機能がどのように関連しているかを判断できます。

-   ユーザーまたはアプリケーションには、従来の関数中心のビューではなく、デバイスを中心としたデバイスのビューが表示されます。

DEVPKEY_Device_ContainerId は、システム内の*devnodes*のデバイスコンテナーグループを決定するために使用できます。 特定の devnode について、次の手順を完了することで、同じコンテナーに属するすべての devnodes を特定できます。

-   Devnode が属しているデバイスコンテナーの**Setupdigetdeviceproperty**値を呼び出します。

-   コンピューター上のすべての devnodes を列挙し、各 devnode の DEVPKEY_Device_ContainerId を照会します。 元の devnode の ContainerId 値に一致する各 ContainerId 値は、同じコンテナーの一部です。

**メモ**   特定のバスの種類のコンテナーに属するすべての*devnodes*は、同じ ContainerID 値を共有する必要があります。

 

ContainerIDs の詳細については、「[コンテナー id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)」を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[コンテナー Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






