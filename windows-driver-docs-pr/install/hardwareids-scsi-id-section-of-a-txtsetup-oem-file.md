---
title: TxtSetup.oem ファイルの HardwareIds.scsi.ID セクション
description: HardwareIds.scsi.ID セクションでは、特定の大容量記憶装置ドライバーがサポートするデバイスのハードウェア Id を指定します。
ms.assetid: 904744d3-524d-42ea-83a8-1fd7e80d07b8
keywords:
- HardwareIds.scsi.ID セクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- HardwareIds.scsi.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f20e1b9087716661b9c10571f13c4bebde526ad9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360602"
---
# <a name="hardwareidsscsiid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルの HardwareIds.scsi.ID セクション


A **HardwareIds.scsi** 。<em>ID</em>セクションでは、特定の大容量記憶装置ドライバーがサポートするデバイスのハードウェア Id を指定します。

``` syntax
[HardwareIds.scsi.ID]
id = "deviceID","service"
...
```

<a href="" id="hardwareids-scsi-id"></a>**HardwareIds.scsi します。** <em>ID</em>  
*ID*に対応する*ID*内のエントリ、 *HwComponent*セクション。

<a href="" id="deviceid"></a>*deviceId*  
大容量記憶装置のデバイス ID を指定します。

<a href="" id="service"></a>*サービス*  
デバイスにインストールされるようにサービスを指定します。 サービスがなく、実行可能イメージのファイル名で指定された、 *.sys*拡張機能。

次の例は抜粋を**HardwareIds.scsi** 。<em>ID</em>ディスク デバイスのセクション。

``` syntax
; ...
[HardwareIds.scsi.oemscsi]
id = "PCI\VEN_9004&DEV_8111","oemscsi"
 
; ... 
```

 

 





