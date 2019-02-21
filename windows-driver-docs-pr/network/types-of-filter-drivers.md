---
title: フィルター ドライバーの種類
description: フィルター ドライバーの種類
ms.assetid: d3a92f10-5f5c-4640-ae03-1bf4e17c45ac
keywords:
- フィルター ドライバー WDK ネットワークの種類
- NDIS フィルター ドライバー WDK、種類
- フィルター ドライバー WDK ネットワークを変更します。
- フィルター ドライバー WDK ネットワークの監視
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b4d0f4da0394470a581c3cc164a951fbb306e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528290"
---
# <a name="types-of-filter-drivers"></a>フィルター ドライバーの種類





フィルター ドライバーには、主に 2 種類があります。

<a href="" id="monitoring"></a>監視  
これらのフィルター ドライバーはドライバー スタックの動作を監視します。 ただし、これらの情報を渡すし、のみドライバー スタックの動作を変更しないでください。 フィルター ドライバーを監視すると、変更または、データを送信できません。

<a href="" id="modifying"></a>変更します。  
これらのフィルター ドライバーはドライバー スタックの動作を変更します。 変更の種類は、ドライバー固有です。

**FilterType** INF ファイルのエントリは、0x00000001 フィルター ドライバーおよびフィルター ドライバーを変更するための 0x00000002 を監視します。

フィルター ドライバーが必須であるを指定することができます。 この機能は通常、フィルター ドライバーの変更に使用されます。 必須のフィルター ドライバーが読み込まれない場合は、関連するドライバー スタックは破棄されます。 必須フィルター ドライバーの詳細については、次を参照してください。[必須フィルター ドライバー](mandatory-filter-drivers.md)します。

 

 





