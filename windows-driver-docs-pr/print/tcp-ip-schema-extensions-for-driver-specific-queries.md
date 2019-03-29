---
title: ドライバー固有クエリの TCP/IP スキーマ拡張
description: ドライバー固有クエリの TCP/IP スキーマ拡張
ms.assetid: c6f85f99-852a-418f-98da-41fe4c36e9ba
keywords:
- TCP/IP スキーマ拡張機能の WDK プリンター
- スキーマ拡張 WDK TCP/IP
- WDK プリンターのドライバー固有のクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3cd7fd6c4eaab33582de07c24b065c5e7b2a44f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578980"
---
# <a name="tcpip-schema-extensions-for-driver-specific-queries"></a>ドライバー固有クエリの TCP/IP スキーマ拡張


前述のように、標準の TCP/IP ポート モニタは、各ドライバーが、クエリを送信し、応答を理解できるように、標準の印刷スキーマのサブセットをサポートします。 ただし、特定のドライバーはプリンターの MIB に格納されている追加の情報を必要があります。

に関する一般的なプリンターのプロパティをクエリを定義するプロパティを含むクエリを作成する必要があります。 次のトピックでは、Tcpbidi.xsd ファイルで定義されている、このような情報を取得する方法を提供する 3 つの構造について説明します。

[const](const.md)

[コンバーター](converter.md)

[インストールされています。](installed2.md)

[値](value.md)

 

 




