---
title: ネットワーク印刷プロバイダーのインストール
description: ネットワーク印刷プロバイダーのインストール
ms.assetid: 448101f8-cb26-4a6f-807d-f110978321da
keywords:
- 印刷プロバイダー、WDK をインストールします。
- ネットワーク印刷プロバイダー、WDK をインストールします。
- 印刷プロバイダー WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa9d20e07c70b47df6e9a1d6eac2940f4a0da0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339075"
---
# <a name="installing-a-network-print-provider"></a>ネットワーク印刷プロバイダーのインストール





新しいネットワーク印刷プロバイダーをインストールするには、ターゲット システムのプロバイダーの DLL をコピーするインストーラーを指定する必要があります\\System32 サブディレクトリに呼び出し**AddPrintProvidor** (Microsoft Windows で説明します。SDK ドキュメントの場合)。 この関数は、プロバイダーのレジストリ エントリを作成し、プロバイダーがインストールされているプロバイダーのスプーラーの一覧の末尾に追加されます。 関数は、プロバイダーの DLL を読み込み、プロバイダーの呼び出し[ **InitializePrintProvidor** ](https://msdn.microsoft.com/library/windows/hardware/ff551614)関数。

ネットワーク印刷プロバイダーでサポートされているプリンターへの接続を作成するには、ユーザーは、プリンターの追加ウィザードを起動し、「ネットワーク プリンター サーバー」オプションを選択します。 ユーザーは、印刷キューを使用して、指定します、 \\ \\ *Server*\\*プリンター*形式、およびプロバイダーの**ようになりました**関数で、印刷キューの名前を認識する必要があります。

 

 




