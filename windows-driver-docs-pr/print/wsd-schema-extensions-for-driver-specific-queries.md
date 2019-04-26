---
title: ドライバー固有クエリの WSD スキーマ拡張
description: ドライバー固有クエリの WSD スキーマ拡張
ms.assetid: 508a9f87-8fd2-4c95-8efb-5d1d7201981a
keywords:
- WSD スキーマ拡張機能の WDK プリンター
- スキーマ拡張 WDK WSD
- WDK プリンターのドライバー固有のクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3eb2b76e34da8f3b025e4905692c1c0cde5992
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355640"
---
# <a name="wsd-schema-extensions-for-driver-specific-queries"></a>ドライバー固有クエリの WSD スキーマ拡張


説明したとおり[プリンター ポート モニターをカスタマイズする](customizing-the-printer-port-monitors.md)、Web サービス Devices (WSD) ポート モニターは、標準のサブセットをサポートしているスキーマの印刷できるように、各ドライバーのクエリを送信し、応答を理解することができます。 ただし、特定のドライバーはプリンターの Web サービスのインターフェイスで使用可能な追加情報を必要があります。

に関する一般的なプリンターのプロパティをクエリでは、定義するプロパティが含まれるクエリを作成する必要があります。 次のトピックでは、次の 4 つのコンストラクト WsdBidi.xsd ファイルで定義されているこのような情報を取得する方法を提供するについて説明します。

[const](const.md)

[インストールされています。](installed.md)

[一覧](list.md)

[値](value.md)

 

 




