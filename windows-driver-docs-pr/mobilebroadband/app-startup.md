---
title: アプリの起動
description: アプリの起動
ms.assetid: 0aca0d3c-9865-4a11-a9c5-e77cc735ba21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3fe25da46f1c4222ca279e66218f9811a934262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351320"
---
# <a name="app-startup"></a>アプリの起動


モバイル ブロード バンド アプリが開始されると、インターネット接続が使用するかどうかを確認する必要があります。 アプリは、インターネット接続のさまざまな状態を検出するのに API を使用できます。 アプリは、バックエンドのデータにアクセスできるかどうか、インターネット接続が「高いガーデン」状態を確認できます。 インターネット接続がない場合、アプリは、ユーザーに、適切なメッセージやオフラインでの作業を表示する必要があります。

複数の演算子のサブスクライバー identity モジュール (Sim) が、PC に接続されている場合、アプリを判断できます。 アプリでは、複数の演算子が接続されているデバイスやアカウントに適しているユーザー インターフェイスを提供する必要があります。

たとえば、アプリはモバイル ブロード バンド デバイスから IMSI と IMEI の情報を読み取ることができます。 この情報は、さらに、またはユーザー名とパスワードの情報をバック エンドに送信されるログオン画面の代わりに、認証方式の一部として使用できます。 Windows では、アプリを使用して、その後、最初のログオン試行後に認証するユーザー名とパスワードの情報を安全に格納するための API を提供します。 すべてのユーザー名とパスワード情報は、Secure HTTP (HTTPS) 演算子のバック エンドと交換される必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのシナリオ](mobile-broadband-app-scenarios.md)

 

 






