---
title: PnP カスタム通知の使用
description: PnP カスタム通知の使用
ms.assetid: de5562f8-07a8-4f4e-ac49-58c789bd9fde
keywords:
- 通知 WDK PnP、カスタム
- カスタム通知 WDK PnP
- 通知 WDK PnP、ターゲットデバイスの変更
- ターゲットデバイスの変更通知の WDK PnP
- Eventカテゴリ Targetdevicechange notification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 282612bb0b101b50e8ecb4a85f773d6be65a7880
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838341"
---
# <a name="using-pnp-custom-notification"></a>PnP カスタム通知の使用





ドライバーは、ターゲットデバイス変更通知メカニズムを使用して、デバイス上のカスタムイベントを通知することができます。

カスタムイベントを定義するプログラマは、次の操作を行う必要があります。

1.  カスタムイベントの新しい GUID を定義します。

    **Uuidgen.exe**または**guidgen.exe** (Microsoft Windows SDK に含まれています) を使用して GUID を生成します。 適切なヘッダーファイルとドキュメントで GUID を発行します。

2.  カスタムイベントをトリガーするコードを記述します。

    カーネルモードでは、ドライバーはカスタム GUID と、デバイスの PDO へのポインターを使用して[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange)を呼び出します。 カスタムイベントは、カーネルモードからのみトリガーできます。

ドライバーライターは、次のような手順でカスタム通知を使用します。

1.  ドライバー (またはアプリケーション) は、カスタムイベントの通知を登録します。

    カーネルモードでは、ドライバーは[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出し、デバイス上の**Eventカテゴリ targetdevicechange**に登録します。

    ユーザーモードでは、アプリケーションは**RegisterDeviceNotification**を使用して登録します。 詳細については、Windows SDK を参照してください。

2.  カーネルモードコンポーネントによって、カスタムイベントがトリガーされます。

3.  PnP マネージャーは、デバイスに登録されている通知ルーチンを呼び出します。

    PnP マネージャーは、登録されているユーザーモードコールバックルーチンを呼び出し、カーネルモードのコールバックルーチンを呼び出します。

4.  ユーザーモードの通知が完了すると、カーネルモードのドライバー通知コールバックルーチンはカスタムイベントに応答します。

    通知コールバックルーチンの一般的なガイドラインについては、「 [PnP 通知コールバックルーチンの記述に関するガイドライン](guidelines-for-writing-pnp-notification-callback-routines.md)」を参照してください。 これらのガイドラインに加えて、カスタム通知コールバックルーチンは、コールバックルーチンスレッド内からデバイスへのハンドルを開くことはできません。

 

 




