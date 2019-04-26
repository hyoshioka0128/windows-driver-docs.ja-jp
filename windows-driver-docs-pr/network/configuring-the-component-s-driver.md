---
title: コンポーネントのドライバーの構成
description: コンポーネントのドライバーの構成
ms.assetid: 0aab9bb0-180c-4e21-ac8e-f20db7e8201a
keywords:
- 通知オブジェクト WDK ネットワー キング、ドライバーの構成
- ネットワーク通知オブジェクト WDK、ドライバーの構成
- ドライバーの構成の WDK ネットワーク コンポーネント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ec533b141834c561c2da8411b2f49ff33a9949
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357435"
---
# <a name="configuring-the-components-driver"></a>コンポーネントのドライバーの構成





後は、ネットワーク構成のサブシステムが通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyPnpChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547726)メソッド、通知オブジェクトの送信先構成情報のドライバーには通知オブジェクトを所有しているネットワーク コンポーネント。 ネットワーク構成のサブシステム呼び出し**ApplyPnpChanges**呼び出した後、 [ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)メソッドとドライバーの後と特定のネットワーク コンポーネントのサービスを開始します。 **ApplyPnpChanges**呼び出し、ネットワーク構成のサブシステムを渡します、 [ **INetCfgPnpReconfigCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547935)インターフェイス。 コンポーネントの通知オブジェクトを使用して、 **INetCfgPnpReconfigCallback**インターフェイスの構成情報をコンポーネントのドライバーに送信します。 このドライバーは、TDI プロバイダーまたは NDIS ミニポート ドライバーのいずれかである必要があります。

通知オブジェクトが呼び出すことができます[ **INetCfgPnpReconfigCallback::SendPnpReconfig** ](https://msdn.microsoft.com/library/windows/hardware/ff547943)内でその**ApplyPnpChanges**構成情報を送信する実装のコンポーネントのドライバーです。 **SendPnpReconfig**ドライバーに構成情報を渡します。

または、通知オブジェクトは、Win32 を呼び出すことができます[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)にそのコンポーネントのドライバーへの接続を開きます。 通知オブジェクトは、Win32 を呼び出すことができます[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)そのコンポーネントのドライバーに直接入力データと共に制御コードを送信します。

通知オブジェクトが使用する必要はありません**INetCfgPnpReconfigCallback**します。 通知オブジェクトを使用する場合は、 **INetCfgPnpReconfigCallback**ユーザーがドライバーで有効にする構成の変更が発生するオペレーティング システムを再起動する必要はありません。

 

 





