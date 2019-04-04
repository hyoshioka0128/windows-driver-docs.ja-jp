---
title: デバイスのインストールの種類
description: Windows では、INF ファイルを使用して、コンピューターまたはデバイス ドライバー パッケージをインストールします。 すべての Windows プラットフォームでは、デスクトップ エディション (Home、Pro、Enterprise、および Education) サポートしているレガシ INF ファイルの Windows 10 のみの中に、ユニバーサル INF ファイルをサポートします。
ms.assetid: 23b999de-7151-4b4a-b9fc-331909bb8c06
keywords:
- デバイス セットアップ WDK デバイス インストールの種類
- デバイスのインストールの種類、WDK
- デバイスの種類、WDK をインストールします。
- サーバー側インストール WDK デバイスのインストール
- クライアント側インストール WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc70de08832eaed9be8af0ff2873add741109ca6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532054"
---
# <a name="device-installation-types"></a>デバイスのインストールの種類


Windows では、INF ファイルを使用して、コンピューターまたはデバイス ドライバー パッケージをインストールします。 すべての Windows プラットフォームでは、デスクトップ エディション (Home、Pro、Enterprise、および Education) サポートしているレガシ INF ファイルの Windows 10 のみの中に、ユニバーサル INF ファイルをサポートします。

## <a name="inf-files-for-universal-and-mobile-driver-packages"></a>ユニバーサルおよびモバイルのドライバー パッケージ用の INF ファイル


ユニバーサルまたはモバイルのドライバー パッケージを作成する場合は、ユニバーサル INF ファイルを指定してください。 ユニバーサル Inf には、INF セクションとをインストールしてデバイスを構成するために必要なディレクティブのサブセットのみが含まれます。 これらのディレクティブは、オフライン システムでは、任意のランタイム操作なしで実行できます。 詳細については、[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)を参照してください。

## <a name="inf-files-for-desktop-driver-packages"></a>デスクトップのドライバー パッケージ用の INF ファイル


デスクトップ専用のドライバー パッケージを作成する場合、INF ファイルでは、レガシ非ユニバーサル INF の構文を使用できます。

Windows 10 デスクトップ エディションの場合は、共同インストーラー クラスのインストーラーなどの従来の INF 動作をサポートするが続行されます。

 

 





