---
title: コンテナーのオーディオのエンドポイント ID
description: オーディオ エンドポイント コンテナー ID のトピックでは、Bluetooth のオーディオ デバイスに関連付けられたオーディオのエンドポイントのコンテナーの ID を取得するため使用できる信頼性の高い方法について説明します。
ms.assetid: 82A852FF-688C-496A-AFF1-C68B0CC1756A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bfd7d30c0922b17748306f16b6eddabf9d1553f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560993"
---
# <a name="audio-endpoint-container-id"></a>コンテナーのオーディオのエンドポイント ID


オーディオ エンドポイント コンテナー ID のトピックでは、Bluetooth のオーディオ デバイスに関連付けられたオーディオのエンドポイントのコンテナーの ID を取得するため使用できる信頼性の高い方法について説明します。

オーディオ エンドポイント ビルダーは、コンテナー、オーディオのエンドポイントの Id を決定する列挙体アルゴリズムを使用し、MMDEVAPI エンドポイントのプロパティ ストアのプロパティとしてこれらの Id を格納します。 場合によってでは、エンドポイント ビルダーによって使用されるロジックはオーディオ オーディオ ドライバーによって公開されるエンドポイントのコンテナー ID が別の列挙子の Bluetooth 列挙子を続く Bluetooth I2S 設計を処理するために十分ではありません。

独自の Bluetooth 列挙子を使用する Bluetooth I2S デザインに関連するこのシナリオはまれです。 ただしに関係なく、このようなシナリオのサポートを提供する、オーディオ ドライバーを開発することができます。 ここで、オーディオ ドライバーでは、エンドポイントに対して新しいコンテナーの ID プロパティをサポートできます。 新しいプロパティが[ **KSPROPERTY\_ジャック\_CONTAINERID** ](https://msdn.microsoft.com/library/windows/hardware/dn265129)とは、既存に追加された[KSPROPSETID\_ジャック](https://msdn.microsoft.com/library/windows/hardware/ff537484)プロパティを設定します。 値は、GUID は、コンテナー ID のデータ型です。

オーディオのドライバー サポート**KSPROPERTY\_ジャック\_CONTAINERID**場合にのみ、その他の手段を使用して適切なコンテナー ID を確実に入手できること、たとえばから Bluetooth の列挙子。

オーディオ ドライバーをサポートしている場合、 **KSPROPERTY\_ジャック\_CONTAINERID**プロパティ、オーディオ システムに、ドライバーからこのプロパティの値がによって読み取られ、ストアのコンテナーとしての値の ID、オーディオエンドポイント。

コンテナー Id と、前のセクションで説明されているアルゴリズムについての詳細については、[コンテナー ID](https://msdn.microsoft.com/library/windows/hardware/ff540024.aspx)と[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)を参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



