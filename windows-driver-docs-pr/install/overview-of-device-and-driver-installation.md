---
title: デバイスとドライバーのインストールの概要
description: デバイスとドライバーのインストールの概要
ms.assetid: 5f29635b-c41b-40d1-8b83-b7f5bc71413b
keywords:
- デバイスのセットアップ WDK デバイスのインストール, デバイスのインストールについて
- デバイスのインストール WDK, デバイスのインストールについて
- デバイスのインストール WDK, デバイスのインストールについて
ms.date: 10/16/2019
ms.localizationpriority: High
ms.openlocfilehash: 284ba5a6913b022a6e7988354388e9e9e76c9abc
ms.sourcegitcommit: c557a56ff865b5766c871e18268637dec455aa89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72512075"
---
# <a name="overview-of-device-and-driver-installation"></a>デバイスとドライバーのインストールの概要

Windows オペレーティング システムでは、システムが再起動するか、ユーザーがプラグ アンド プレイ (PnP) デバイスをプラグイン (または手動でインストール) するときに、デバイスがインストールされます。

具体的には、Windows はシステム内に存在するデバイスを列挙し、各デバイスのドライバーを読み込んで呼び出します。

ACPI ドライバーやその他の PnP [バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)などのドライバーにより、Windows はどのデバイスが存在するかを判断しやすくなります。

## <a name="in-this-section"></a>このセクションの内容


-   [手順 1: 新しいデバイスが識別される](step-1--the-new-device-is-identified.md)
-   [手順 2:デバイスのドライバーが選択される](step-2--a-driver-for-the-device-is-selected.md)
-   [手順 3:デバイスのドライバーがインストールされる](step-3--the-driver-for-the-device-is-installed.md)
-   [ドライバーの選択プロセスの概要](overview-of-the-driver-selection-process.md)

