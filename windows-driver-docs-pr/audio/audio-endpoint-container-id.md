---
title: オーディオ エンドポイント コンテナー ID
description: オーディオ エンドポイント コンテナー ID のトピックでは、Bluetooth のオーディオ デバイスに関連付けられたオーディオのエンドポイントのコンテナーの ID を取得するため使用できる信頼性の高い方法について説明します。
ms.assetid: 82A852FF-688C-496A-AFF1-C68B0CC1756A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3860db8dd4138f14a63487b880dcf34bfeb52d7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355701"
---
# <a name="audio-endpoint-container-id"></a>オーディオ エンドポイント コンテナー ID


オーディオ エンドポイント コンテナー ID のトピックでは、Bluetooth のオーディオ デバイスに関連付けられたオーディオのエンドポイントのコンテナーの ID を取得するため使用できる信頼性の高い方法について説明します。

オーディオ エンドポイント ビルダーは、コンテナー、オーディオのエンドポイントの Id を決定する列挙体アルゴリズムを使用し、MMDEVAPI エンドポイントのプロパティ ストアのプロパティとしてこれらの Id を格納します。 場合によってでは、エンドポイント ビルダーによって使用されるロジックはオーディオ オーディオ ドライバーによって公開されるエンドポイントのコンテナー ID が別の列挙子の Bluetooth 列挙子を続く Bluetooth I2S 設計を処理するために十分ではありません。

独自の Bluetooth 列挙子を使用する Bluetooth I2S デザインに関連するこのシナリオはまれです。 ただしに関係なく、このようなシナリオのサポートを提供する、オーディオ ドライバーを開発することができます。 ここで、オーディオ ドライバーでは、エンドポイントに対して新しいコンテナーの ID プロパティをサポートできます。 新しいプロパティが[ **KSPROPERTY\_ジャック\_CONTAINERID** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-containerid)とは、既存に追加された[KSPROPSETID\_ジャック](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-jack)プロパティを設定します。 値は、GUID は、コンテナー ID のデータ型です。

オーディオのドライバー サポート**KSPROPERTY\_ジャック\_CONTAINERID**場合にのみ、その他の手段を使用して適切なコンテナー ID を確実に入手できること、たとえばから Bluetooth の列挙子。

オーディオ ドライバーをサポートしている場合、 **KSPROPERTY\_ジャック\_CONTAINERID**プロパティ、オーディオ システムに、ドライバーからこのプロパティの値がによって読み取られ、ストアのコンテナーとしての値の ID、オーディオエンドポイント。

コンテナー Id と、前のセクションで説明されているアルゴリズムについての詳細については、次を参照してください。[コンテナー ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)と[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



