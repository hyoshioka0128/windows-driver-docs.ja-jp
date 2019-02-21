---
title: WindowsInfo XML ドキュメント
description: WindowsInfo XML ドキュメント
ms.assetid: 8004d165-46c5-4bf4-849d-ba83205b9f54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ebc8266c4e0cb16f0c735cda6dea0ebfab2506
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550352"
---
# <a name="windowsinfo-xml-document"></a>WindowsInfo XML ドキュメント


このドキュメントには、デバイス メタデータ パッケージの指定したデバイスのオペレーティング システムを実行するアクションを表示を指定するデータが含まれています。 必要となる操作には、次のようなものがあります。

-   かどうか、[デバイス アイコン](device-icon-file.md)と、デバイスは、ユーザーがデバイスを削除する場合など、切断の状態が表示されます。 このアクションがで指定された、 [ **ShowDeviceInDisconnectedState** ](https://msdn.microsoft.com/library/windows/hardware/ff552242) WindowsInfo XML ドキュメント内の XML 要素。

-   かどうか、デバイスが切断状態から、デバイスのユーザーとはプラグインなどの接続の状態に遷移するときは、Device Stage ユーザー インターフェイスが表示されます。 このアクションがで指定された、 [ **LaunchDeviceStageOnDeviceConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff548633) WindowsInfo XML ドキュメント内の XML 要素。

-   ユーザーがダブルクリックしたときに、Device Stage ユーザー インターフェイスを起動するかどうか、[デバイス アイコン](device-icon-file.md)デバイスとプリンターのいずれかのユーザー インターフェイスで、または Windows エクスプ ローラーで表示されます。 このアクションがで指定された、 [ **LaunchDeviceStageFromExplorer** ](https://msdn.microsoft.com/library/windows/hardware/ff548629) WindowsInfo XML ドキュメント内の XML 要素。

各デバイス メタデータ パッケージは、1 つだけの WindowsInfo XML ドキュメントを含める必要があります。 ドキュメントの名前である必要があります*WindowsInfo.xml*します。

WindowsInfo XML ドキュメント内のデータはに基づいて書式設定、 [WindowsInfo XML スキーマ](https://msdn.microsoft.com/library/windows/hardware/ff553992)します。

 

 





