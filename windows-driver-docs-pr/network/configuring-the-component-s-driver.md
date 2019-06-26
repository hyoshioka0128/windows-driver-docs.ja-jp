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
ms.openlocfilehash: b9cd025e96efd0694f6eff539f81686def1e8364
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374980"
---
# <a name="configuring-the-components-driver"></a>コンポーネントのドライバーの構成





後は、ネットワーク構成のサブシステムが通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))メソッド、通知オブジェクトの送信先構成情報のドライバーには通知オブジェクトを所有しているネットワーク コンポーネント。 ネットワーク構成のサブシステム呼び出し**ApplyPnpChanges**呼び出した後、 [ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))メソッドとドライバーの後と特定のネットワーク コンポーネントのサービスを開始します。 **ApplyPnpChanges**呼び出し、ネットワーク構成のサブシステムを渡します、 [ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))インターフェイス。 コンポーネントの通知オブジェクトを使用して、 **INetCfgPnpReconfigCallback**インターフェイスの構成情報をコンポーネントのドライバーに送信します。 このドライバーは、TDI プロバイダーまたは NDIS ミニポート ドライバーのいずれかである必要があります。

通知オブジェクトが呼び出すことができます[ **INetCfgPnpReconfigCallback::SendPnpReconfig** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547943(v=vs.85))内でその**ApplyPnpChanges**構成情報を送信する実装のコンポーネントのドライバーです。 **SendPnpReconfig**ドライバーに構成情報を渡します。

または、通知オブジェクトは、Win32 を呼び出すことができます[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)にそのコンポーネントのドライバーへの接続を開きます。 通知オブジェクトは、Win32 を呼び出すことができます[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)そのコンポーネントのドライバーに直接入力データと共に制御コードを送信します。

通知オブジェクトが使用する必要はありません**INetCfgPnpReconfigCallback**します。 通知オブジェクトを使用する場合は、 **INetCfgPnpReconfigCallback**ユーザーがドライバーで有効にする構成の変更が発生するオペレーティング システムを再起動する必要はありません。

 

 





