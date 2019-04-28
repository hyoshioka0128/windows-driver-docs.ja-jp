---
title: 位置情報ドライバー サンプルのインストール
description: 地理的位置情報ドライバー サンプルでは、ハードウェアをシミュレート、ために、インストールを自動化するプラグ アンド プレイ機能はありません。 サンプルをインストールするのに Windows ユーティリティ、devcon.exe が代わりに、使用する必要があります。
ms.assetid: A08EA9B0-E1D6-47AE-BD89-C43D7D817DAF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40cca5ae13c929345f9409de21fcdf0a0043b125
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371032"
---
# <a name="installing-the-geolocation-driver-sample"></a>位置情報ドライバー サンプルのインストール

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

地理的位置情報ドライバー サンプルでは、ハードウェアをシミュレート、ために、インストールを自動化するプラグ アンド プレイ機能はありません。 サンプルをインストールするのに Windows ユーティリティ、devcon.exe が代わりに、使用する必要があります。

次の手順では、インストール プロセスを説明します。

1.  ドライバーがエラーなしでビルドされることを確認します。

2.  2. テスト コマンドを実行して署名を有効にする"bcdedit に testsigning を設定/"管理者特権でコマンド プロンプトからです。 (テスト署名を有効にした後、コンピューターを再起動する必要あります)。
3.  別のフォルダーに、ドライバーの DLL と INF ファイルをコピーします。

4.  再頒布可能パッケージ/wdf から 2 つの共同インストーラー DLL ファイル (checked または無料) を検索/*プロセッサ\_型*WDK をインストールしたフォルダーです。 手順 3 で作成したフォルダーには、これらのファイルをコピーします。 たとえば、ドライブ C に WDK をインストールする場合は、WUDFUpdate をコピー可能性があります\_c: から 01009.dll\\WinDDK\\*ビルド\#*\\redist\\wdf\\x86。

5.  Devcon.exe を実行します。 ツールでこのプログラムを見つけることができます\\WDK をインストールした devcon フォルダー。 たとえば、センサー WDKExample という名前では、入力します。

    **devcon.exe インストール WDKExample.inf"センサー\\WDKExample"**

    **注**  にリリースされたドライバーをインストールする Devcon.exe を使用しないでください。 この推奨事項はテストのみです。

     

## <a name="related-topics"></a>関連トピック
[センサー地理位置情報ドライバー サンプル](sensors-geolocation-driver-sample.md)  



