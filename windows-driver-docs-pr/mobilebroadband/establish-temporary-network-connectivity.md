---
title: 一時的なネットワーク接続を確立する
description: 一時的なネットワーク接続を確立する
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff0a3a43aec6a585a67c4a44a74ce05d7ce734c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380171"
---
# <a name="establish-temporary-network-connectivity"></a>一時的なネットワーク接続を確立する


電気通信のアプリケーションでは、長期的な接続を開始できません。 ただし、特定のネットワークに一時的な接続が必要な場合、モバイル ブロード バンド API を次のように使用できます。

1.  インスタンスを作成[ **IMbnConnectionManager**](https://msdn.microsoft.com/library/windows/desktop/dd430380)します。

2.  登録する、 [ **IMbnConnectionEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd430375)接続ポイント。

3.  インスタンスを作成[ **IMbnInterfaceManager**](https://msdn.microsoft.com/library/windows/desktop/dd430416)します。

4.  取得、 [ **IMbnInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430406)にアカウントのデバイス ID を渡すことによって、デバイスのインターフェイス[ **IMbnInterfaceManager::GetInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430420). (詳細については、次を参照してください[、デバイスのロック解除](unlock-a-device.md)。)。

5.  デバイスの IMbnConnection インターフェイスを呼び出すことによって取得[ **IMbnConnectionManager::GetConnection**](https://msdn.microsoft.com/library/windows/desktop/dd430384)します。

6.  呼び出して接続を確立[ **IMbnConnection::Connect**](https://msdn.microsoft.com/library/windows/desktop/dd430399)します。 *ConnectionMode*にパラメーターを設定する必要があります**MBN\_接続\_モード\_TMP\_プロファイル**、および*strProfile*パラメーターは、モバイル ブロード バンドのプロファイルの説明をする必要があります。

使用して、接続試行の結果が返されます、 [ **IMbnConnectionEvents::OnConnectComplete** ](https://msdn.microsoft.com/library/windows/desktop/dd430376)メソッド。 呼び出しが完了したらを切断する、 [ **IMbnConnection::Disconnect** ](https://msdn.microsoft.com/library/windows/desktop/dd430401)メソッド。 使用して状態が返されます[ **IMbnConnectionEvents::OnDisconnectComplete**](https://msdn.microsoft.com/library/windows/desktop/dd430378)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






