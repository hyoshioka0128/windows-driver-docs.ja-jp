---
title: WindowsInfo XML ドキュメント
description: WindowsInfo XML ドキュメント
ms.assetid: 8004d165-46c5-4bf4-849d-ba83205b9f54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c82e9b27cafd05599f97ae38d36d7a1492e7698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363506"
---
# <a name="windowsinfo-xml-document"></a>WindowsInfo XML ドキュメント


このドキュメントには、デバイス メタデータ パッケージの指定したデバイスのオペレーティング システムを実行するアクションを表示を指定するデータが含まれています。 必要となる操作には、次のようなものがあります。

-   かどうか、[デバイス アイコン](device-icon-file.md)と、デバイスは、ユーザーがデバイスを削除する場合など、切断の状態が表示されます。 このアクションがで指定された、 [ **ShowDeviceInDisconnectedState** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff552242(v=vs.85)) WindowsInfo XML ドキュメント内の XML 要素。

-   かどうか、デバイスが切断状態から、デバイスのユーザーとはプラグインなどの接続の状態に遷移するときは、Device Stage ユーザー インターフェイスが表示されます。 このアクションがで指定された、 [ **LaunchDeviceStageOnDeviceConnect** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548633(v=vs.85)) WindowsInfo XML ドキュメント内の XML 要素。

-   ユーザーがダブルクリックしたときに、Device Stage ユーザー インターフェイスを起動するかどうか、[デバイス アイコン](device-icon-file.md)デバイスとプリンターのいずれかのユーザー インターフェイスで、または Windows エクスプ ローラーで表示されます。 このアクションがで指定された、 [ **LaunchDeviceStageFromExplorer** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548629(v=vs.85)) WindowsInfo XML ドキュメント内の XML 要素。

各デバイス メタデータ パッケージは、1 つだけの WindowsInfo XML ドキュメントを含める必要があります。 ドキュメントの名前である必要があります*WindowsInfo.xml*します。

WindowsInfo XML ドキュメント内のデータはに基づいて書式設定、 [WindowsInfo XML スキーマ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff553992(v=vs.85))します。

 

 





