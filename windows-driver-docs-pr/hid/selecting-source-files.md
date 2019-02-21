---
title: ソース ファイルの選択
description: ソース ファイルの選択
ms.assetid: 259a7092-1197-4521-853a-6064aaa0c037
keywords:
- INF ファイル WDK ジョイスティック、ソース ファイルします。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b50448289795d5be097fda85eefd76212b2eea1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528127"
---
# <a name="selecting-source-files"></a>ソース ファイルの選択





INF ファイルの"SourceDisksFiles"セクションでは、コピーするファイルを指定します。 これには、すべての必要なドライバーのドキュメントとセットアップ アプリケーションなど、他のファイルも含まれます。 これはユーザーのシステムにインストールする最初のジョイスティック ドライバーを指定して、Vjoyd.vxd と Msjstrick.drv システム ジョイスティックのドライバーをコピーするだけでなくこのデバイスの特定のドライバーです。 これら 2 つのドライバーのソースを Layout.inf (Windows 95/98/Me インストール ディスクが求められないように、ユーザーの原因) への参照を確立して、OEM のディスクに分散されていない必要があります。ドライバーは、接続先のコード 11 は、ユーザーのシステム ディレクトリにコピーする必要があります。

 

 




