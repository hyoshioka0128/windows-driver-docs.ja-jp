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
ms.openlocfilehash: 2dffd766a2ab27bd678d675dee9a5e949ce5a91e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385975"
---
# <a name="installing-a-network-print-provider"></a>ネットワーク印刷プロバイダーのインストール





新しいネットワーク印刷プロバイダーをインストールするには、ターゲット システムのプロバイダーの DLL をコピーするインストーラーを指定する必要があります\\System32 サブディレクトリに呼び出し**AddPrintProvidor** (Microsoft Windows で説明します。SDK ドキュメントの場合)。 この関数は、プロバイダーのレジストリ エントリを作成し、プロバイダーがインストールされているプロバイダーのスプーラーの一覧の末尾に追加されます。 関数は、プロバイダーの DLL を読み込み、プロバイダーの呼び出し[ **InitializePrintProvidor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintprovidor)関数。

ネットワーク印刷プロバイダーでサポートされているプリンターへの接続を作成するには、ユーザーは、プリンターの追加ウィザードを起動し、「ネットワーク プリンター サーバー」オプションを選択します。 ユーザーは、印刷キューを使用して、指定します、 \\ \\ *Server*\\*プリンター*形式、およびプロバイダーの**ようになりました**関数で、印刷キューの名前を認識する必要があります。

 

 




