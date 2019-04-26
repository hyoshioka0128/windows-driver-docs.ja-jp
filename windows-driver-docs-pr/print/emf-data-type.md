---
title: EMF データ型
description: EMF データ型
ms.assetid: d5a05778-3637-4dba-b036-5f0fc236d52d
keywords:
- プリント プロセッサ WDK、データ型
- WDK のデータ型のプリント プロセッサ
- EMF データ型の WDK のプリント プロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e49ba1551df5753088de2cdba9463113b0d94e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343196"
---
# <a name="emf-data-type"></a>EMF データ型





拡張メタファイル (EMF) データは、GDI 関数を呼び出す手順で構成されます。 プリント プロセッサは、印刷可能なイメージを表示するために、GDI 関数を呼び出す必要があります。 GDI 関数は、プリンター ドライバーの呼び出しを行う[プリンター グラフィックス DLL](printer-graphics-dll.md)、イメージをレンダリングし、生データとして、スプーラーに送信します (呼び出して[ **EngWritePrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff565467)).

オペレーティング システムの NT ベースのクライアントは、プリント サーバー、NT ベースのオペレーティング システムに EMF データを送信します。 EMF データは、デバイスに依存しないと、生データよりも迅速に、サーバーに送信されることができます。 印刷ジョブは、要求元のアプリケーションが、スプーラーのバック グラウンド スレッドで EMF データが表示される、その後、アプリケーションにすばやく戻り値を許可するサーバーのローカル EMF データとしてもスプールされます。

EMF のデータ型の詳細については、次を参照してください。、 *Windows 2000 Professional リソース キット*または*Windows 2000 Server Resource Kit*します。 拡張メタファイルの詳細については、Windows SDK のドキュメントを参照してください。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 




