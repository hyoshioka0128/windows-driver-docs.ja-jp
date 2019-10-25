---
title: シリアル デバイスの読み取り/書き込みのタイムアウトを設定する
description: シリアル デバイスの読み取り/書き込みのタイムアウトを設定する
ms.assetid: ed5b80a9-93cb-4e3f-9038-e715be35f206
keywords:
- Serial driver WDK、タイムアウト
- タイムアウト WDK シリアルデバイス
- シリアルデバイス WDK、タイムアウト
- 読み取りタイムアウト WDK シリアルデバイス
- ライトタイムアウト WDK シリアルデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d7990770ae3ed4134bf26c1b92830bdaac1a32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845387"
---
# <a name="setting-read-and-write-timeouts-for-a-serial-device"></a>シリアル デバイスの読み取り/書き込みのタイムアウトを設定する

クライアントは、 [**IOCTL\_serial\_set\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求を使用して、システムによって提供される serial .sys ドライバーが読み取り要求と書き込み要求に使用するタイムアウト値を設定できます。 シリアル .sys は、要求されたバイト数が転送されるか、タイムアウトイベントが発生するまでバイトを転送し続けます。

Serial .sys のタイムアウト操作は、Microsoft Windows SDK 内の Windows ベースサービスでサポートされている通信機能によってサポートされる[COM ポート](configuration-of-com-ports.md)のユーザーモード操作に準拠しています。

タイムアウト操作は、キューに入っている間、保留中の要求には適用されないことに注意してください。 タイムアウト操作は、要求が現在の状態になった後に、要求に適用されます (つまり、シリアル .sys は要求の処理を開始します)。

読み取りと書き込みのタイムアウトの詳細については、次を参照してください。

- Windows Driver Kit (WDK) の Ntddser ヘッダーファイル内の[**シリアル\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)構造体。

- [**Setcommtimeouts**](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setcommtimeouts)関数と、Windows SDK の Windows ベースサービスでサポートされている[**commタイムアウト**](https://docs.microsoft.com/windows/desktop/api/winbase/ns-winbase-_commtimeouts)構造体。
