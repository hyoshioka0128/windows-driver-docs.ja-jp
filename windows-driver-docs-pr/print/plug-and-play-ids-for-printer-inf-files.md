---
title: プリンター INF ファイルのプラグ アンド プレイ ID
description: プリンター INF ファイルのプラグ アンド プレイ ID
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- WDK の INF ファイルを印刷するプラグ アンド プレイ Id
- 印刷の PnP ID WDK
- プラグ アンド プレイ Id WDK を印刷します。
- 識別子の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17bb9ee5619d8d224b7f179c192f409e5ecadb7f
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181252"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>プリンター INF ファイルのプラグ アンド プレイ ID

指定する必要があります[プラグ アンド プレイ](plug-and-play-for-printers.md)(PnP) 識別子 (Id) で、[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)します。

プリンターが使用するプロトコルに応じて、次の表に、Id を使用する必要があります。

|プロトコル|プリンター INF ファイルでの PnP ID。|
|----|----|
|IEEE 1394|ID が固有で、ID 文字列で「1394」では常にします。|
|Parallel|ID には、ID 文字列で"LPTENUM"が含まれています。|
|USB|ID には、ID 文字列で"USBPRINT"が含まれています。|
|Dot4|ID には、ID 文字列で"DOT4PRT"が含まれています。 この ID は、Dot4USB と並列に適用されます。|
|Bluetooth|ID には、ID 文字列で"BTHPRINT"が含まれています。|
|WSD|ID には、ID 文字列で"WSDPRINT"が含まれています。|
