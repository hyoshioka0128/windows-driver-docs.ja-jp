---
title: フラットベッド スキャナーのミニドライバーのサンプル
description: フラットベッド スキャナーのミニドライバーのサンプル
ms.assetid: 8c1ad90a-cff9-45a0-b2d9-e2605436f128
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f87a4e80ceb6be62e781990a80d06286b57a028
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378402"
---
# <a name="flatbed-scanner-minidriver-sample"></a>フラットベッド スキャナーのミニドライバーのサンプル





*Wiascanr* Windows DDK のディレクトリにドキュメント フィーダーの付いたフラット ベッド スキャナーのサンプル WIA ミニドライバーが含まれています。

このサンプルでは、スキャナー用 WIA ユーザー モードのミニドライバーを作成する方法を示します。 テスト パターンのイメージを生成してスキャンをシミュレートします。 このサンプル ドライバーは、開発の開始点として使用できますが、ドライバーは、カーネル モード ドライバーを Windows に付属のいずれかで、スキャナーのハードウェアにアクセスする必要があります。 推奨されるカーネル モード ドライバーが*usbscan.sys*と*scsiscan.sys*します。

### <a name="sample-features"></a>サンプルの機能

-   自動ドキュメント フィーダー付きの機能

    このサンプルでは、自動ドキュメント フィーダー (ADF) のフラット ベッド スキャナーとスクロールが取り込まれるスキャナー (ページの長さを決定することはできませんフィーダー) の例を示します。

-   スキャン、コピー、および Fax ボタンのサポート (中断イベント)

    小規模なアプリケーションを実行*Scanpanl.exe* (これは Windows DDK に付属) ボタンを押すようをシミュレートするためにします。

 

 




