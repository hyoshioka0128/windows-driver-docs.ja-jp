---
title: INF ファイルを作成する
description: INF ファイルを作成する
ms.assetid: c45fb42c-f0d6-4ab8-9a19-4bbf98c4cf8c
keywords:
- ジョイスティックに WDK を非表示に INF ファイル
- 仮想ジョイスティックのドライバー WDK を非表示に INF ファイル
- VJoyD WDK HID、INF ファイル
- INF ファイル WDK ジョイスティック
- INF ファイル WDK のジョイスティックを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 295fbf690cfbc271105a04fe09c7fd38d9a564ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578983"
---
# <a name="creating-an-inf-file"></a>INF ファイルを作成する





システムに必要なすべての情報を提供する INF ファイルを使用して、すべてのミニドライバーと OEM 定義のジョイスティックをインストールする必要があります。 INF ファイルには、デバイス、ファイルをコピーする必要があります、互換性のある任意のデバイス、デバイスを必要として、レジストリへの変更のすべてのシステム リソースのクラスの観点からデバイスのインストールについて説明します。 標準のアナログのドライバーをカスタマイズするための INF ファイルは、任意のファイル、互換性のあるデバイスの状態をコピーまたはシステム リソースを指定する必要はありません。 INF ファイルは、Autoexec.bat ファイルの変更など、他のアクションを指定できますが、これは、ジョイスティック ミニドライバーの通常必要ありません。

INF ファイルには、次のトピックで説明する要素が含まれています。

[デバイス クラスの設定](setting-the-device-class.md)

[ソース ファイルの選択](selecting-source-files.md)

[製造元固有のデータを設定](setting-the-manufacturer-specific-data.md)

[LogConfig エントリの設定](setting-up-logconfig-entries.md)

[AddReg エントリの設定](setting-up-addreg-entries.md)

 

 




