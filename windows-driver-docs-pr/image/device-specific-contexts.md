---
title: デバイス固有のコンテキスト
description: デバイス固有のコンテキスト
ms.assetid: 29e0d451-57fb-4943-9508-022adffa4650
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 997a393dadee38d8f955e3f4b81a60dd3cc975ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570308"
---
# <a name="device-specific-contexts"></a>デバイス固有のコンテキスト





ミニドライバーと必要に応じて、デバイスに固有の情報を格納するためのプライベート コンテキストを使用します。 このデバイスに固有のコンテキストでは、時間、ミニドライバーがデバイスの情報を取得するデバイスを呼び出す必要がありますの数を減らすことができます。 特定のミニドライバーのドライバーの項目ごとに 1 つだけのデバイス固有のコンテキストがあります。 ドライバーの項目が不要、WIA サービス呼び出しミニドライバーの[ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543972)すべてのデバイスに固有にアタッチされているリソースを解放しますコンテキスト。

たとえば、カメラ ドライバーは、デバイスからサムネイルのデータを取得するとき、通常はキャッシュ適切なドライバーの項目に関連付けられているドライバーのコンテキストでのデータします。 WIA サービスが、コンテキストを解放することに注意してください。 ドライバーの責任では、そのコンテキストによって保持されているすべてのリソースを解放することです。 場合は、前の例のサムネイルのデータが格納されたデバイスに固有のコンテキストで割り当てられたメモリのキャッシュされたデータをメモリ保持しているがコンテキスト自体ではありませんが、ここでは、解放必要があります。

 

 




