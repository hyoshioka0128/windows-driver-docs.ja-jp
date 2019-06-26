---
title: DEVPKEY_Device_ContainerId
description: DEVPKEY_Device_ContainerId
ms.assetid: 9d5be913-b699-4d8f-aa3f-53ad5dbe6482
keywords:
- DEVPKEY_Device_ContainerId デバイスとドライバーのインストール
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
ms.openlocfilehash: c1c8347e5395fa5caa7385dd01364c1ef3c3101a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387083"
---
# <a name="devpkeydevicecontainerid"></a>DEVPKEY_Device_ContainerId


DEVPKEY_Device_ContainerId のデバイス プロパティは、1 つまたは複数のデバイス ノードをグループ化するプラグ アンド プレイ (PnP) manager で使用 (*devnode*) に、*デバイス コンテナー*の物理インスタンスを表すデバイスです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ContainerId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows 7 以降、PnP マネージャーを使用してデバイス コンテナーとその識別子 (*ContainerID*) を 1 つまたは複数のグループに*devnode*から発生したこと、および特定の各インスタンスに属しています。物理デバイス。 デバイス インスタンス ContainerID は DEVPKEY_Device_ContainerId デバイス プロパティを通じて参照されます。

コンテナーに 1 つのデバイスのインスタンスで発生したすべての devnode をグループ化する場合は、次の結果を実現します。

-   オペレーティング システムの間で機能をどのように関連するかを確認できます*devnode*物理デバイスから発信されます。

-   ユーザーまたはアプリケーションの従来の関数を中心としたビューではなくデバイスのデバイス中心のビューが表示されます。

DEVPKEY_Device_ContainerId は特定のデバイスのコンテナーのグループ化に使用できる*devnode*システム。 指定された devnode の次の手順を実行して同じコンテナーに属するすべての devnode を特定できます。

-   呼び出す**SetupDiGetDeviceProperty**その devnode が所属するデバイスのコンテナーの値。

-   コンピューター上のすべての devnode を列挙し、その DEVPKEY_Device_ContainerId 各 devnode を照会します。 元の devnode ContainerId 値と一致する各 ContainerId 値は、同じコンテナーの一部です。

**注**  すべて*devnode*コンテナーに属するバス上の種類が同じ ContainerID 値を共有する必要があります。

 

ContainerIDs の詳細については、次を参照してください。[コンテナー Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[コンテナー Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






