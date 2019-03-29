---
title: リムーバブル デバイスの機能からコンテナー Id を生成する方法
description: リムーバブル デバイス機能でコンテナー ID を生成する方法
ms.assetid: 493a9473-4989-4557-b2b2-efa0e2a8b24e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aaae8db2d5bbcbd1c7103d93f0aed3ee19d728e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572071"
---
# <a name="how-container-ids-are-generated-from-the-removable-device-capability"></a>リムーバブル デバイス機能でコンテナー ID を生成する方法


バス ドライバーがデバイス ノードのコンテナー ID を提供できないかどうか (*devnode*) の列挙、プラグ アンド プレイ (PnP) マネージャーでは、リムーバブル デバイスの機能を使用して、デバイスの列挙されたすべての devnode のコンテナー ID を生成することです。 リムーバブル デバイスの機能の詳細については、次を参照してください。[リムーバブル デバイスの機能の概要](overview-of-the-removable-device-capability.md)します。

次のヒューリスティックでは、リムーバブル デバイスの機能からコンテナー Id を生成する方法について説明します。

1.  Devnode に設定するリムーバブル デバイスの機能を持つかどうか**TRUE**devnode の新しいコンテナー ID を生成します。

2.  Devnode に設定するリムーバブル デバイスの機能を持つかどうか**FALSE**、コンテナー ID をその親 devnode から継承します。

初期化されるまで、devnode は子 devnode を列挙できませんし、その*ドライバー スタック*が開始します。 初期化中に、コンテナー ID が割り当てられるとすぐに devnode が列挙されるまでその他の子のいずれかのコンテナー ID を伝達する準備ができます。

設定するリムーバブル デバイス機能を持つ devnode **TRUE**この devnode の ID が生成されたコンテナーと、デバイスの最上位の (親) devnode と見なされます。

設定、リムーバブル デバイスの機能を自身がない限り、この親 devnode のすべての子が同じコンテナー ID を継承**TRUE**します。 この場合、リムーバブル子 devnode は別のコンテナー ID が割り当てられているし、このリムーバブル デバイスの親 devnode になります。 その devnode のすべての子が同じコンテナー ID を継承します。

たとえば、単一関数のマウスが USB 経由でコンピューターに接続されているとします。 この場合は、USB バス ドライバーでは、新しいデバイスを検出し、USB ヒューマン インターフェイス デバイス (HID) があることを検出します。 USB バス ドライバーは、デバイスの USB HID devnode を作成します。 HID devnode もが検出された HID デバイス マウス HID 準拠のマウスの子 devnode を作成します。

この例の結果で、次の操作には、このヒューリスティックを適用します。

1.  USB HID devnode が作成されます。 リムーバブル デバイスの機能に設定されている**TRUE**この devnode でその親の USB ハブ devnode ことを認識するためが、社外と接している USB ポートに接続されました。

2.  コンテナー ID は、リムーバブル デバイスの最上位の devnode のため、この devnode 作成されます。 その結果、この devnode は、リムーバブル デバイスの親 devnode と見なされます。

3.  HID 準拠のマウス devnode が作成されます。 リムーバブル デバイスの機能に設定されている**FALSE**この devnode でその親の USB HID devnode として他のすべての子を報告するためです。 この場合は、HID 準拠のマウス devnode は親 devnode のコンテナーの ID を継承します。

このヒューリスティックでは、使用は、同じコンテナー ID は、マウスが属している各 devnode に割り当てられます。 PnP マネージャーが正常にグループ化、devnode 論理デバイスの場合は、デバイスの一意識別子がない場合でもです。

**注**  このヒューリスティックの成功を列挙できる各 devnode のリムーバブル デバイスの機能を正しく報告される特定のバス ドライバーに依存しています。 バス ドライバー確認することとして、リムーバブル デバイスの親 devnode を設定する必要があり、その子 devnode は設定しないでリムーバブルとあります。

 

 

 





