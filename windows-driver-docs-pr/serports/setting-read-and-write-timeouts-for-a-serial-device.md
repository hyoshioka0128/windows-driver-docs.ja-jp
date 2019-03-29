---
title: シリアル デバイスの読み取り/書き込みのタイムアウトを設定する
description: シリアル デバイスの読み取り/書き込みのタイムアウトを設定する
ms.assetid: ed5b80a9-93cb-4e3f-9038-e715be35f206
keywords:
- シリアル ドライバー WDK、タイムアウト
- タイムアウトの WDK シリアル デバイス
- シリアル デバイス WDK、タイムアウト
- タイムアウトの WDK シリアル デバイスを読み取る
- タイムアウト WDK シリアル デバイスを書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7576f6bda821226044325bd87028643a413f907c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570788"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>シリアル デバイスの読み取り/書き込みのタイムアウトを設定する





クライアントが使用できる、 [ **IOCTL\_シリアル\_設定\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/ff546772)読み取りと書き込みのため、システム提供の際にドライバーを使用するタイムアウト値を設定する要求要求します。 要求されたバイト数が転送されるか、タイムアウト イベントが発生するまでのバイトを転送する際に続行されます。

以下のように、タイムアウトの操作がユーザー モードの操作を準拠[COM ポート](configuration-of-com-ports.md)Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信関数でサポートされています。

キューに配置中に、タイムアウトの操作は保留中の要求に適用されないことに注意してください。 タイムアウトの操作が要求を要求が最新になった後に適用 (要求を処理する際に起動時は、)。

読み取りと書き込みのタイムアウトの詳細については、次を参照してください。

-   [**シリアル\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/hh439614) Ntddser.h ヘッダー ファイルで、Windows Driver Kit (WDK) で構造体。

-   [ **SetCommTimeouts** ](https://msdn.microsoft.com/library/windows/desktop/aa363437)関数と[ **COMMTIMEOUTS** ](https://msdn.microsoft.com/library/windows/desktop/aa363190)構造の Windows ベースのサービスでサポートされている、Windows SDK。

 

 




