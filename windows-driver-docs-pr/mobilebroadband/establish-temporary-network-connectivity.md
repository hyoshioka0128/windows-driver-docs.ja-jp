---
title: 一時的なネットワーク接続を確立する
description: 一時的なネットワーク接続を確立する
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d2d37126c25185b20435bc3ef9e9085f228dba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381469"
---
# <a name="establish-temporary-network-connectivity"></a>一時的なネットワーク接続を確立する


電気通信のアプリケーションでは、長期的な接続を開始できません。 ただし、特定のネットワークに一時的な接続が必要な場合、モバイル ブロード バンド API を次のように使用できます。

1.  インスタンスを作成[ **IMbnConnectionManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionmanager)します。

2.  登録する、 [ **IMbnConnectionEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionevents)接続ポイント。

3.  インスタンスを作成[ **IMbnInterfaceManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)します。

4.  取得、 [ **IMbnInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)にアカウントのデバイス ID を渡すことによって、デバイスのインターフェイス[ **IMbnInterfaceManager::GetInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface). (詳細については、次を参照してください[、デバイスのロック解除](unlock-a-device.md)。)。

5.  デバイスの IMbnConnection インターフェイスを呼び出すことによって取得[ **IMbnConnectionManager::GetConnection**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionmanager-getconnection)します。

6.  呼び出して接続を確立[ **IMbnConnection::Connect**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-connect)します。 *ConnectionMode*にパラメーターを設定する必要があります**MBN\_接続\_モード\_TMP\_プロファイル**、および*strProfile*パラメーターは、モバイル ブロード バンドのプロファイルの説明をする必要があります。

使用して、接続試行の結果が返されます、 [ **IMbnConnectionEvents::OnConnectComplete** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-onconnectcomplete)メソッド。 呼び出しが完了したらを切断する、 [ **IMbnConnection::Disconnect** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-disconnect)メソッド。 使用して状態が返されます[ **IMbnConnectionEvents::OnDisconnectComplete**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-ondisconnectcomplete)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






