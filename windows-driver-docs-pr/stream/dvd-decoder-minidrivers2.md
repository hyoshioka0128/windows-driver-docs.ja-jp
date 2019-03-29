---
title: DVD デコーダーのミニドライバー
description: DVD デコーダーのミニドライバー
ms.assetid: 1dec271d-47cf-4ab6-9149-7f5b9b92b189
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、DVD デコーダー ミニドライバー
- モデルの WDK Windows 2000 カーネル、DVD デコーダー ミニドライバーのストリーミング
- カーネル ストリーミング モデルの WDK、DVD デコーダー ミニドライバー
- DVD デコーダー ミニドライバー WDK
- デコーダー ミニドライバー WDK DVD
- ビデオ再生の WDK DVD デコーダー
- オーディオの平均的 WDK DVD デコーダー
- ビデオの再生 WDK DVD デコーダー
- 再生 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32203fa7e859a19a4056f92b1e2b386e9eda5444
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571624"
---
# <a name="dvd-decoder-minidrivers"></a>DVD デコーダーのミニドライバー





DVD は、オーディオ、ビデオ、およびその他のデジタル データを含むデジタル データ ストレージを提供します。 このドキュメントでは、DVD からムービー再生 (ビデオおよびオーディオ) に使用される DVD デコーダー ミニドライバーの設計について説明します。 これらのミニドライバーは、DVD デコーダー アダプター カードの読み取りおよび mpeg-2 (ビデオおよびオーディオ)、ac-3 DTS など DVD データ ストリームの形式のデコードを制御します。

Stream クラス ドライバーを使用した DVD デコーダー ミニドライバー インターフェイスです。 これにより、すべてのデータ型の動作を 1 つのドライバー モデルを使用して、ストリーム クラスでビルドする多機能デバイス用のドライバーを作成する開発者 (mpeg-2、ac-3、DTS、)。

DVD デコーダー ミニドライバーは移植性があり、同期を提供するストリーム クラス ドライバーを使用している場合マルチプロセッサの問題点がありません。 MPEG - 2 で、オーディオ ドライバーのさまざまなモデルを使用して個別のドライバーを作成する開発者が、以前は、MIDI、およびサブピクチャします。 詳細については、次を参照してください。[ストリーミング ミニドライバー](streaming-minidrivers2.md)します。

次のトピックについて説明します。

[Windows での DVD デコーダーのサポート](dvd-decoder-support-in-windows.md)

[DVD のデータ ストリーム](dvd-data-streams.md)

[DVD の著作権保護](dvd-copyright-protection.md)

[DVD 加入](dvd-regionalization.md)

[マスター クロック](master-clock.md)

 

 




