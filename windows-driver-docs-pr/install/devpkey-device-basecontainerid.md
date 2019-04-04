---
title: DEVPKEY_Device_BaseContainerId
description: DEVPKEY_Device_BaseContainerId
ms.assetid: ccc20b78-60a3-4351-9809-e2a285ad0a19
keywords:
- DEVPKEY_Device_BaseContainerId デバイスとドライバーのインストール
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
ms.openlocfilehash: 2bb33eda4fbf0c898e3b69c32df217ae97726fa4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556601"
---
# <a name="devpkeydevicebasecontainerid"></a>DEVPKEY_Device_BaseContainerId


DEVPKEY_Device_BaseContainerId デバイス プロパティを表します、 *GUID*基本のコンテナー識別子の値 (*ID*)。Windows プラグ アンド プレイ (PnP) マネージャーでは、[デバイス] ノードにこの値を割り当てます (*devnode*)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BaseContainerId</p></td>
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
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_BASE_CONTAINERID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

PnP マネージャーでは、次のメソッドのいずれかを使用して devnode のコンテナーの ID を決定します。

-   バス ドライバーは、コンテナー ID を提供します。

    PnP マネージャーでは、コンテナー ID を割り当てる devnode に、まず devnode のバス ドライバーがコンテナー ID を指定できるかどうか バス ドライバーを通じてコンテナー ID を提供する、 [ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)クエリ要求を**Parameters.QueryId.IdType**フィールドに設定**BusQueryContainerID**します。

-   PnP マネージャーでは、リムーバブル デバイスの機能を使用して、コンテナー ID が生成されます。

    バス ドライバーは、列挙 devnode のコンテナーの ID を提供することはできません、PnP マネージャーは、デバイスに列挙されているすべての devnode のコンテナー ID を生成するのにリムーバブル デバイスの機能を使用します。 バス ドライバーへの応答でこのデバイスの機能の報告、 [ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)要求。

-   PnP マネージャーでは、リムーバブル デバイスの機能のオーバーライドを使用してコンテナー ID を生成します。

    優先機構はリムーバブル デバイスの機能の値を変更していない、強制的に、PnP マネージャー デバイス用のコンテナーの Id を生成するときに、上書きの設定とリムーバブル デバイスの機能の値ではなくを使用する作成されます。

これらのメソッドの詳細については、[どのコンテナー Id が生成される](https://msdn.microsoft.com/library/windows/hardware/ff546193)を参照してください。

コンテナーの ID 値を取得する方法に関係なく、PnP マネージャーは devnode の DEVPKEY_Device_BaseContainerId プロパティに値を割り当てます。

その他のシステムに存在する devnode で新しい devnode のグループ化を強制する DEVPKEY_Device_BaseContainerId プロパティを使用できます。 これにより、親として新しい devnode を使用できます (または*基本*) その他のコンテナーの ID に関連する devnode します。 これを行うには、まず既存の devnode の DEVPKEY_Device_BaseContainerID GUID を入手する必要があります。 次に、応答で、コンテナーの新しい devnode ID GUID を返す必要がある、 [ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)クエリ要求を持つ、 **Parameters.QueryId.IdType**フィールドに設定**BusQueryContainerID**します。

**注**   、DEVPKEY_Device_BaseContainerId のクエリによって返される値または[ **DEVPKEY_Device_ContainerId** ](devpkey-device-containerid.md)プロパティが同じ devnode 異なることが.

 

**注**  DEVPKEY_Device_BaseContainerId プロパティ システムにデバイス コンテナー グループを再構築を使わないでください。 使用して、 [ **DEVPKEY_Device_ContainerId** ](devpkey-device-containerid.md)プロパティ代わりにします。

 

コンテナー Id の詳細については、[コンテナー Id](https://msdn.microsoft.com/library/windows/hardware/ff540024)を参照してください。

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


[コンテナー Id](https://msdn.microsoft.com/library/windows/hardware/ff540024)

[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






