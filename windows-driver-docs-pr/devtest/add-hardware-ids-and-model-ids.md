---
title: デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
description: デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
ms.assetid: 1BF563AE-B37B-4105-BA76-2D13F88B2BBD
keywords:
- デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e77e7073e38b0cd567b058fe8e11b30803f30aa2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332061"
---
# <a name="add-hardware-and-model-ids-in-the-device-metadata-authoring-wizard"></a>デバイス メタデータ作成ウィザードでのハードウェア ID とモデル ID の追加


ハードウェア Id では、bus 固有の値に基づくハードウェアの機能を識別して、デバイス ドライバーをデバイスにマップするために使用できます。 たとえば、同じハードウェア ID を持つ 2 つのデバイスは、同じドライバーによって使用される機能インターフェイスを共有します。 デバイス メタデータ パッケージを特定のバスまたはインターフェイス上のデバイスのインスタンスにマップするハードウェア Id が使用されます。

モデル Id は、バスまたはインターフェイスのテクノロジの独立した物理デバイスを一意に識別するには、Original Equipment Manufacturer (OEM) または独立系ハードウェア ベンダー (IHV) を許可します。 たとえば、別のモデル Id を持つ 2 つのデバイスには、そのコンポーネントの同じハードウェア Id があります。 デバイス メタデータ パッケージをデバイスがコンピューターに接続する方法に関係なく、物理デバイスにマップするモデル Id が使用されます。

デバイス メタデータ パッケージのハードウェア Id およびモデルの Id を関連付けるにはクリックして、**アソシエーション**タブ。

### <a name="span-idtoaddahardwareidspanspan-idtoaddahardwareidspanspan-idtoaddahardwareidspanto-add-a-hardware-id"></a><span id="To_add_a_Hardware_ID_"></span><span id="to_add_a_hardware_id_"></span><span id="TO_ADD_A_HARDWARE_ID_"></span>ハードウェア ID を追加するには

1.  をクリックして、**アソシエーション**タブ。
2.  横に**ハードウェア ID**、クリックして、**プラス記号 (+)** します。
3.  表示されるボックスで、ハードウェア ID を入力します
    **注**  会社のベンダーの id を格納する値を使用して、可能であれば、。 次に、例を示します。USB\\VID\_045E &AMP; PID\_0047

     

4.  **[OK]** をクリックします。

### <a name="span-idtoaddamodelidspanspan-idtoaddamodelidspanspan-idtoaddamodelidspanto-add-a-model-id"></a><span id="To_add_a_Model_ID_"></span><span id="to_add_a_model_id_"></span><span id="TO_ADD_A_MODEL_ID_"></span>モデル ID を追加するには

1.  をクリックして、**アソシエーション**タブ。
2.  横に**モデル ID**、クリックして、**プラス記号 (+)** します。
3.  表示されるボックスで、モデル ID の GUID 値を入力します。
4.  **[OK]** をクリックします。

各デバイスのスタイルのハードウェア ID の詳細については、次を参照してください。、[デバイス メタデータ パッケージ スキーマ リファレンス for Windows 8](https://go.microsoft.com/fwlink/p/?LinkId=226753)します。

 

 





