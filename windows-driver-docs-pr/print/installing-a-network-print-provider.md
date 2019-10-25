---
title: ネットワーク印刷プロバイダーのインストール
description: ネットワーク印刷プロバイダーのインストール
ms.assetid: 448101f8-cb26-4a6f-807d-f110978321da
keywords:
- 印刷プロバイダー WDK、インストール
- ネットワーク印刷プロバイダー WDK、インストール
- 印刷プロバイダー WDK のインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa1291646a5c139ef4b0f5e1a31fc234b44c0504
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832104"
---
# <a name="installing-a-network-print-provider"></a>ネットワーク印刷プロバイダーのインストール





新しいネットワーク印刷プロバイダーをインストールするには、プロバイダー DLL をターゲットシステムの \\System32 サブディレクトリにコピーするインストーラーを指定してから、 **Addprintの Dor**を呼び出します (Microsoft Windows SDK のドキュメントを参照してください)。 この関数は、プロバイダーのレジストリエントリを作成し、インストールされているプロバイダーのスプーラの一覧の末尾にプロバイダーを追加します。 次に、この関数はプロバイダー DLL を読み込み、プロバイダーの[**Initializeprintdor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)関数を呼び出します。

ネットワーク印刷プロバイダーでサポートされているプリンターへの接続を作成するには、ユーザーがプリンターの追加ウィザードを起動し、[ネットワークプリンターサーバー] オプションを選択します。 ユーザーは \\\\*Server*\\*プリンター*形式を使用して印刷キューを指定します。また、プロバイダーの**OpenPrinter**関数は、その印刷キュー名を認識している必要があります。

 

 




