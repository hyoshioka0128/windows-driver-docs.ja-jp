---
title: MFP のデバイス機能を識別する
description: MFP のデバイス機能を識別する
ms.assetid: 14016c43-b93a-4009-848b-1bcf3f1d94b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c040bfae10bdc7c27884a91e62902ea730b3e665
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419556"
---
# <a name="identifying-device-functions-in-mfps"></a>MFP のデバイス機能を識別する

デバイスとプリンターのユーザー インターフェイスは、MFP に属するプリンターとスキャナーの関数を識別するためにデバイス コンテナー id (ContainerID) を使用します。 ContainerID、機能のデバイスですべてのインスタンス (devnode)、MFP などの多機能デバイスが同じ多機能デバイスの一部として識別するために使用できる GUID です。 たとえば、プリンターの機能のデバイスのインスタンスと、MFP でスキャナー機能デバイス インスタンス ContainerID 値が同じである必要があります。

デバイス レポート ContainerID.If デバイスでは、ContainerID、Windows PnP デバイスのいずれかを割り当てますは報告されません。 Windows PnP は、多くの多機能デバイスではある多機能デバイス全体を表す、親デバイス、および、多機能の個々 の関数を表す子デバイスという事実を利用してこの id を実行しますデバイスです。 PnP マネージャーでは、機能するデバイスの 2 つのインスタンスが同じ親を持つと、リムーバブル デバイスとしてどちらのインスタンスが見つかった場合は、2 つのインスタンスによって、永続的なメンバーに同じ多機能デバイスのある必要がありますを前提としています。 この手法を使用すると、Windows PnP は、デバイスの機能のインスタンスに共通 ContainerIDs を割り当てることができます。

1 つ以上のトランスポート経由で接続がデバイスの場合 (つまり、デバイスが接続と WSD の USB 経由)、デバイスが 1 つのデバイスとして表示する別のデバイスのインスタンスを作成、ContainerID をレポートすることをお勧めします。

ContainerIDs の詳細については、[コンテナー ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)を参照してください。
