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
ms.openlocfilehash: b9f584efeab0f858ebb42551d4439edf5525a965
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356735"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>シリアル デバイスの読み取り/書き込みのタイムアウトを設定する

クライアントが使用できる、 [ **IOCTL\_シリアル\_設定\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)読み取りと書き込みのため、システム提供の際にドライバーを使用するタイムアウト値を設定する要求要求します。 要求されたバイト数が転送されるか、タイムアウト イベントが発生するまでのバイトを転送する際に続行されます。

以下のように、タイムアウトの操作がユーザー モードの操作を準拠[COM ポート](configuration-of-com-ports.md)Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信関数でサポートされています。

キューに配置中に、タイムアウトの操作は保留中の要求に適用されないことに注意してください。 タイムアウトの操作が要求を要求が最新になった後に適用 (要求を処理する際に起動時は、)。

読み取りと書き込みのタイムアウトの詳細については、次を参照してください。

- [**シリアル\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts) Ntddser.h ヘッダー ファイルで、Windows Driver Kit (WDK) で構造体。

- [ **SetCommTimeouts** ](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setcommtimeouts)関数と[ **COMMTIMEOUTS** ](https://docs.microsoft.com/windows/desktop/api/winbase/ns-winbase-_commtimeouts)構造の Windows ベースのサービスでサポートされている、Windows SDK。
