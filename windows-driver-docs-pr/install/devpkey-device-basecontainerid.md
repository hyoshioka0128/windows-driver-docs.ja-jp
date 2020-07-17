---
title: DEVPKEY_Device_BaseContainerId
description: DEVPKEY_Device_BaseContainerId
ms.assetid: ccc20b78-60a3-4351-9809-e2a285ad0a19
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_BaseContainerId
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BaseContainerId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c288741b17c1bf085859c6e770d566f9d24e1eb0
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418278"
---
# <a name="devpkey_device_basecontainerid"></a>DEVPKEY_Device_BaseContainerId


DEVPKEY_Device_BaseContainerId デバイスプロパティは、ベースコンテナー識別子 (*ID*) の*GUID*値を表します。Windows プラグアンドプレイ (PnP) マネージャーによって、この値がデバイスノード (*devnode*) に割り当てられます。

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
<td align="left"><p>DEVPKEY_Device_BaseContainerId</p></td>
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
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_BASE_CONTAINERID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

PnP マネージャーは、次のいずれかの方法を使用して、devnode のコンテナー ID を決定します。

-   バスドライバーは、コンテナー ID を提供します。

    PnP マネージャーは、devnode にコンテナー ID を割り当てると、まず、devnode のバスドライバーがコンテナー ID を提供できるかどうかを確認します。 バスドライバーは、 [**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)クエリ要求を通じてコンテナー ID を提供します。 **QueryId**フィールドは**busquerycontainerid**に設定されています。

-   PnP マネージャーは、リムーバブルデバイスの機能を使用して、コンテナー ID を生成します。

    バスドライバーが列挙されている devnode のコンテナー ID を提供できない場合、PnP マネージャーはリムーバブルデバイス機能を使用して、デバイス用に列挙されているすべての devnodes のコンテナー ID を生成します。 バスドライバーは、 [**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求に応答してこのデバイス機能を報告します。

-   PnP マネージャーは、リムーバブルデバイスの機能のオーバーライドを使用して、コンテナー ID を生成します。

    上書きメカニズムによってリムーバブルデバイスの機能の値が変更されることはありませんが、デバイスのコンテナー Id を生成するときに、リムーバブルデバイスの機能の値ではなく、強制的に PnP マネージャーによって上書き設定が使用されるように強制されます。

これらのメソッドの詳細については、「[コンテナー id の生成方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)」を参照してください。

コンテナー ID の値を取得する方法に関係なく、PnP マネージャーは devnode の [DEVPKEY_Device_BaseContainerId] プロパティに値を割り当てます。

DEVPKEY_Device_BaseContainerId プロパティを使用して、システムに存在する他の devnodes と新しい devnode のグループ化を強制することができます。 これにより、新しい devnode を他の関連する devnodes の親 (または*基本*) コンテナー ID として使用できるようになります。 これを行うには、最初に既存の devnode の DEVPKEY_Device_BaseContainerID GUID を取得する必要があります。 次に、 **QueryId**フィールドが**busquerycontainerid**に設定されている[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)クエリ要求に応答して、新しい devnode のコンテナー ID GUID を返す必要があります。

**メモ**   DEVPKEY_Device_BaseContainerId または[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)プロパティのクエリによって返される値は、同じ devnode に対して異なる場合があります。

 

**メモ**   DEVPKEY_Device_BaseContainerId プロパティを使用して、システム内のデバイスコンテナーグループを再構築しないでください。 代わりに、 [**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)プロパティを使用してください。

 

コンテナー Id の詳細については、「[コンテナー id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)」を参照してください。

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

[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






