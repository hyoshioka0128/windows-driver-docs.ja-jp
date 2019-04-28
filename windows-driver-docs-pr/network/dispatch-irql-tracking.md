---
title: ディスパッチ IRQL の追跡
description: ディスパッチ IRQL の追跡
ms.assetid: ac559f4f-0138-4b9a-8f1b-44a2973fd6a1
keywords:
- ディスパッチ レベルのフラグの WDK ネットワーク
- Irql WDK ネットワーク
- ネットワーク ドライバー WDK、Irql
- 現在の Irql WDK ネットワーク
- WDK のネットワー キングの追跡の IRQL をディスパッチします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86f23825ef547a60fb480a81d41529c1efa0c6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379563"
---
# <a name="dispatch-irql-tracking"></a>ディスパッチ IRQL の追跡





一部の NDIS 関数、システムのパフォーマンスを向上させるために (たとえば、 [ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)関数)、ディスパッチ レベルを示すフラグ現在の IRQL にはが含まれます。 適切なディスパッチ レベルのフラグの使用は、IRQL を設定しようと不要なを回避するのに役立ちます。

他の属性を制御するその他のフラグがディスパッチ レベルのフラグの名前。

NDIS\_送信\_フラグ\_ディスパッチ\_レベル

NDIS\_送信\_完了\_フラグ\_ディスパッチ\_レベル

NDIS\_受信\_フラグ\_ディスパッチ\_レベル

NDIS\_返す\_フラグ\_ディスパッチ\_レベル

NDIS\_RWL\_で\_ディスパッチ\_レベル

呼び出し元は、IRQL のテストではなく既知の現在の IRQL からディスパッチ レベルのフラグ設定を決定する必要があります。 たとえば、ドライバーの設計の固定特性か、ドライバーは、現在の IRQL を保存のための IRQL がわかります。

既知の現在の IRQL がディスパッチ場合\_レベル、呼び出し元はこのフラグを設定する必要があります。 現在の IRQL が不明、または呼び出し元がディスパッチで実行されていない場合\_レベル、呼び出し元はこのフラグをクリアする必要があります。 呼び出し元が NDIS の場合は、呼び出された関数する必要があります、IRQL の変更を回避するには、このフラグをテストします。

ディスパッチのレベルのフラグの値を決定する IRQL のドライバーをテストしないでください。 テスト フラグの目的が無意味になります。 必要に応じて、呼び出された関数には、テスト自体。 ドライバーが必要がありますまたはフラグを設定する必要がありますを決定する方法は、特定のドライバーの設計にままです。

 

 





