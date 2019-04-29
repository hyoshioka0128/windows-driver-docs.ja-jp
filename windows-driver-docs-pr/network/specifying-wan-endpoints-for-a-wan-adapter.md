---
title: WAN アダプターの WAN エンドポイントの指定
description: WAN アダプターの WAN エンドポイントの指定
ms.assetid: e6dd12c3-03e3-4f7d-8ad7-2511bf46c4f8
keywords:
- 追加レジストリ セクション WDK、WAN ネットワーク アダプターのエンドポイント
- WAN アダプター エンドポイント WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e22610913c44b8aff40210aa29ef42e3150a2322
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388115"
---
# <a name="specifying-wan-endpoints-for-a-wan-adapter"></a>WAN アダプターの WAN エンドポイントの指定





WAN アダプターの INF ファイルを追加する必要があります、 **WanEndpoints**値をアダプターのインスタンス キー。 **WanEndpoints** 21\_WAN アダプターによってサポートされているエンドポイント (チャネル、回線またはベアラー チャネルとも呼ばれます) の数を指定する DWORD の値。 たとえば、 **WanEndpoints**の値を*基本速度インターフェイスの*一方、(BRI) の ISDN アダプターは、2、 **WanEndpoints**の値を*プライマリ速度インターフェイス*(PRI) の ISDN アダプターは、通常は 23 です。

**注**   ISDN ドライバーが Windows 8.1、Windows Server 2012 R2 で非推奨とそれ以降。

 

例を次に、*追加レジストリ セクション*を追加する、 **WanEndpoints** BRI ISDN アダプターの 2 の値。

```INF
[a1.reg]
HKR,, WanEndpoints, 0x00010001, 2
```

 

 





