---
title: デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
description: デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
ms.assetid: 1BF563AE-B37B-4105-BA76-2D13F88B2BBD
keywords:
- デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec93357dc51fa5c5dea5c036d28e9ac22e8aab1b
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769410"
---
# <a name="add-hardware-and-model-ids-in-the-device-metadata-authoring-wizard"></a>デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加


ハードウェア Id は、バス固有の値に基づいてハードウェアの機能を識別し、デバイスドライバーをデバイスにマップするために使用できます。 たとえば、同じハードウェア ID を持つ2つのデバイスは、同じドライバーによって使用される機能インターフェイスを共有します。 ハードウェア Id は、デバイスメタデータパッケージを特定のバスまたはインターフェイスのデバイスインスタンスにマップするために使用されます。

モデル Id を使用すると、相手先ブランド供給 (OEM) または独立系ハードウェアベンダー (IHV) は、バスやインターフェイスのテクノロジに依存しない物理デバイスを一意に識別できます。 たとえば、異なるモデル Id を持つ2つのデバイスは、そのコンポーネントに対して同じハードウェア Id を持つことができます。 モデル Id は、デバイスがコンピューターに接続する方法に関係なく、デバイスメタデータパッケージを物理デバイスにマップするために使用されます。

デバイスメタデータパッケージのハードウェア Id とモデル Id を関連付けるには、[**関連付け**] タブをクリックします。

### <a name="span-idto_add_a_hardware_id_spanspan-idto_add_a_hardware_id_spanspan-idto_add_a_hardware_id_spanto-add-a-hardware-id"></a><span id="To_add_a_Hardware_ID_"></span><span id="to_add_a_hardware_id_"></span><span id="TO_ADD_A_HARDWARE_ID_"></span>ハードウェア ID を追加するには

1.  [**関連付け**] タブをクリックします。
2.  [**ハードウェア ID**] の横に**あるプラス記号 (+)** をクリックします。
3.  表示されるボックスに、ハードウェア ID を入力します。
    **メモ**   可能であれば、会社のベンダー ID を含む値を使用します。 例: USB \\ VID \_ 045e&PID \_ 0047

     

4.  **[OK]** をクリックします。

### <a name="span-idto_add_a_model_id_spanspan-idto_add_a_model_id_spanspan-idto_add_a_model_id_spanto-add-a-model-id"></a><span id="To_add_a_Model_ID_"></span><span id="to_add_a_model_id_"></span><span id="TO_ADD_A_MODEL_ID_"></span>モデル ID を追加するには

1.  [**関連付け**] タブをクリックします。
2.  [**モデル ID**] の横に**あるプラス記号 (+)** をクリックします。
3.  表示されたボックスに、モデル ID の GUID 値を入力します。
4.  **[OK]** をクリックします。

各デバイススタイルのハードウェア ID の詳細については、「[デバイスメタデータパッケージの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-metadata-packages)」を参照してください。

 

 





