---
title: NetAdapterCx クライアント ドライバーの電源のシーケンス
description: NetAdapterCx クライアント ドライバーの電源のシーケンス
ms.assetid: 9E16172C-9E45-4ED7-B6D2-7539DF4718B5
keywords:
- NetAdapterCx クライアント ドライバーの電源のシーケンス
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48635d5c7bb5decb13c6a7c69da2f2db7e31ced7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537328"
---
# <a name="power-down-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの電源のシーケンス

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図は、電源を切ったとき、NetAdapterCx クライアント ドライバーのイベントのコールバック関数を呼び出す順序とデバイスを削除します。 シーケンスは、図の上部にある作業の電源の状態 (D0) では、運用のデバイスで始まります。

<img src="images/netadaptercx-powerdown.png" alt="Device enumeration and power-down sequence for NetAdapterCx client driver" title="デバイスの列挙と NetAdapterCx クライアント ドライバーの電源のシーケンス" style="width: 600px;"/>

広範な水平の線は、デバイスの電源に関連するステップをマークします。 図の左側にある列について、手順を説明し、右側の列には、そのイベントのコールバックが一覧表示されます。 青色のテキストでマークされている手順は、他の手順はすべて WDF ベースのドライバーに共通 NetAdapterCx に固有です。

図が示すよう電源と削除のシーケンスでは、デバイスを運用に関連する関数がフレームワークと呼ばれる逆の順序で、対応する「元に戻す」コールバックを呼び出す必要があります。 フレームワークは、デバイス オブジェクトのコンテキストの領域を削除した後にデバイス オブジェクトを削除します。
