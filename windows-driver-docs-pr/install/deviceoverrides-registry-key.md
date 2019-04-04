---
title: DeviceOverrides レジストリ キー
description: DeviceOverrides レジストリ キー
ms.assetid: 18f95848-71fe-4884-bcbe-d3cae90fc262
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d2f2a5abc278d3679ecb57bd1b8d084dc2f992e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531019"
---
# <a name="deviceoverrides-registry-key"></a>DeviceOverrides レジストリ キー


Windows 7 以降、 **DeviceOverrides**レジストリ キーは、1 つまたは複数のリムーバブル デバイス機能の上書きがシステムに存在することを指定します。 リムーバブル デバイスの機能の詳細については、[リムーバブル デバイスの機能の概要](overview-of-the-removable-device-capability.md)を参照してください。

プラグ アンド プレイ (PnP) マネージャーでは、発生元をコンピューターにインストールされている特定の物理デバイスの各インスタンスに属する新しい ID (コンテナー Id) を使用します。 レガシ デバイスの場合は、PnP マネージャーは、リムーバブル デバイスの機能を通じてコンテナー Id を生成します。 PnP マネージャーが、コンテナー Id がどのように生成するかについての詳細については、[どのコンテナー Id が生成される](how-container-ids-are-generated.md)を参照してください。

独立系ハードウェア ベンダー (IHV) または供給 (OEM) devnode または devnode のグループにリムーバブル デバイスの機能の解釈された値を変更してリムーバブル デバイスの機能の上書きを使用できます。

リムーバブル デバイスの機能のオーバーライドを**DeviceOverrides**レジストリ キーは従来のデバイスやリムーバブル デバイスの機能が正しく報告がサード パーティ製ハードウェア コンポーネントに便利です。 これにより、ID が物理デバイスから列挙 devnode をグループ化に使用するコンテナーを正しく生成 PnP マネージャーです。

これらのオーバーライドは、devnode によって報告されたリムーバブル デバイスの機能のグローバル状態を実際には変更しないでください。 代わりに、これらの上書きが発生する、PnP マネージャー報告されるデバイスの機能を無視し、生成するときに、レジストリ ベースの設定を使用する、[コンテナー ID](container-ids.md) devnode オーバーライドに一致するのです。 DeviceOverrides レジストリ サブキーの下の他のサブキーは、オーバーライドするには、どの devnode について詳細を説明します。

次の表の定義、 **DeviceOverrides**レジストリ キーの形式と要件。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ キーの名前</th>
<th align="left">必須/省略可能</th>
<th align="left">形式の要件</th>
<th align="left">親キー</th>
<th align="left">子のサブキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>DeviceOverrides</strong></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a>または<a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
</tr>
</tbody>
</table>

 

いずれかで各リムーバブル デバイスの機能のオーバーライドが指定されて、 **HardwareID**または**ContainerID**レジストリ サブキー。

**DeviceOverrides**レジストリ キーの作成し、管理は、、 [HKLM\\システム\\CurrentControlSet\\コントロール レジストリ ツリー](hklm-system-currentcontrolset-control-registry-tree.md)します。 このレジストリ キー内で 1 つまたは複数のリムーバブル デバイス機能の上書きを作成または維持されます。

リムーバブル デバイスの機能の上書きがいずれかで指定された個々 のデバイスに固有の[HardwareID](hardwareid-registry-subkey.md)または[CompatibleID](compatibleid-registry-subkey.md)レジストリ サブキー。 その他のサブキーは、devnode は特定のデバイス列挙のパスを定義します。 一般より一般的なハードウェアではなく、または互換性のある、デバイスを識別する ID を使用する必要がありますに最も固有のデバイスのハードウェアの id。 これにより、同じハードウェアまたは目的のターゲット デバイスと互換性のある ID を共有するすべての意図しないデバイスに、リムーバブル デバイスの機能の上書きが適用されません。

次の図のトポロジ、 **DeviceOverrides**レジストリ キーおよびその関連のサブキー。

![deviceoverrides レジストリ キー トポロジを示す図](images/containerid-3.png)

**DeviceOverrides**システムに追加される最初のリムーバブル デバイス機能のオーバーライドのレジストリ キーを作成する必要があります。 既定では、オペレーティング システムのクリーン インストールでない可能性があります。

**注**  リムーバブル デバイスの機能のレジストリ上書きが存在するには、devnode でリムーバブル デバイスの機能のグローバル状態は変わりません。

 

 

 





