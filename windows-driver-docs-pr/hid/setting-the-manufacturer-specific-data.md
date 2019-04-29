---
title: 製造元固有のデータを設定
description: 製造元固有のデータを設定
ms.assetid: 57787e7a-2a80-476c-8027-b7c154b2f407
keywords:
- INF ファイルを WDK のジョイスティックの製造元に固有のデータ
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba6fda05386abdcfb7c4b350ba4287e84b4ced56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384367"
---
# <a name="setting-the-manufacturer-specific-data"></a>製造元固有のデータを設定





INF ファイルを指す製造元固有のセクションには、インストールできるデバイスごとに 1 つのエントリが含まれています。 各エントリには、インストール セクション、デバイス ID、および任意の互換性のあるデバイスの名前の後にデバイスの名前が含まれています。 プラグ アンド プレイ対応として、デバイスを登録している場合、(以降、アスタリスクで) プラグ アンド プレイ ID を使用のデバイス id。 デバイスが登録されていない、プラグ アンド プレイ互換性のある (つまり、1 つで始まっていない場合は、アスタリスク) ではないデバイス ID を使用する必要があります。 この種類のデバイスを登録するときに、他のデバイス Id と競合する ID を選択しないでください。 ("ジョイスティック、"などはできません、適切な ID)。

 

 




