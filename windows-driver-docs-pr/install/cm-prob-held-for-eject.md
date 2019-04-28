---
title: CM_PROB_HELD_FOR_EJECT
description: CM_PROB_HELD_FOR_EJECT
ms.assetid: 8d67ad71-276d-4dea-b3fb-61fedcfba789
keywords:
- CM_PROB_HELD_FOR_EJECT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2b0c9d11d69a885f4ca447ee78f4235702461a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360316"
---
# <a name="cmprobheldforeject"></a>CM_PROB_HELD_FOR_EJECT

この関数は、システムの使用に予約されています。

取り出し、デバイスが用意されています。

## <a name="error-code"></a>エラー コード

47

### <a name="display-message"></a>メッセージを表示します。

"Windows デバイスを使用できませんこのハードウェア '安全な取り外し' が用意されていますが、コンピューターから削除されていないためです。 (コード 47)"

「この問題を解決するには、お使いのコンピューターから取り外すし、再度接続のみです。」

### <a name="recommended-resolution"></a>推奨される解決方法

デバイスを取り外し、再び接続します。 または、選択**コンピューターの再起動**がコンピューターを再起動し、デバイスを使用できるようにします。

ユーザーを削除するデバイスを準備するホット プラグ プログラムを起動している場合にのみ、このエラーが発生する必要があります (呼び出す[ **CM_Request_Device_Eject**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_request_device_ejectw))、ユーザーが物理の取り出しを押したかどうかまたは (ボタン呼び出し[ **IoRequestDeviceEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdeviceeject))。 ユーザーでは、現在、ラップトップとドッキング ステーション トレイ間でトラップ CD-ROM などのリムーバブル デバイスを準備できます。
