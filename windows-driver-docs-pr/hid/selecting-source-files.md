---
title: ソース ファイルの選択
description: ソース ファイルの選択
ms.assetid: 259a7092-1197-4521-853a-6064aaa0c037
keywords:
- INF ファイル WDK ジョイスティック、ソース ファイルします。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b50448289795d5be097fda85eefd76212b2eea1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345455"
---
# <a name="selecting-source-files"></a>ソース ファイルの選択





INF ファイルの"SourceDisksFiles"セクションでは、コピーするファイルを指定します。 これには、すべての必要なドライバーのドキュメントとセットアップ アプリケーションなど、他のファイルも含まれます。 これはユーザーのシステムにインストールする最初のジョイスティック ドライバーを指定して、Vjoyd.vxd と Msjstrick.drv システム ジョイスティックのドライバーをコピーするだけでなくこのデバイスの特定のドライバーです。 これら 2 つのドライバーのソースを Layout.inf (Windows 95/98/Me インストール ディスクが求められないように、ユーザーの原因) への参照を確立して、OEM のディスクに分散されていない必要があります。ドライバーは、接続先のコード 11 は、ユーザーのシステム ディレクトリにコピーする必要があります。

 

 




