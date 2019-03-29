---
title: WHEA 対応のユーザーモード アプリケーションの概要
description: WHEA 対応のユーザーモード アプリケーションの概要
ms.assetid: cf2de8fa-191b-4dae-aaac-5d6d74f94ca7
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、ユーザー モード アプリケーション
- WHEA WDK、ユーザー モード アプリケーション
- ハードウェア エラー WDK WHEA、ユーザー モード アプリケーション
- WDK WHEA、ユーザー モード アプリケーションのエラー
- ユーザー モード アプリケーション WDK WHEA
- WDK WHEA イベント
- WDK WHEA、カテゴリのイベント
- Windows ハードウェア エラー アーキテクチャ WDK のイベント
- WHEA WDK、イベント
- ハードウェア エラー WDK WHEA、イベント
- WDK WHEA、イベントのエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aab35dafdf21cbf19fc90489f991a6773ac6897
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578361"
---
# <a name="introduction-to-whea-aware-user-mode-applications"></a>WHEA 対応のユーザーモード アプリケーションの概要


Windows ハードウェア エラー アーキテクチャ (WHEA) は、ユーザー モード アプリケーション WHEA ハードウェア エラーのイベントを処理し、WHEA 管理操作を実行するためのメカニズムを提供します。

WHEA のハードウェア エラーのイベントの処理は、2 つのカテゴリに分類されます。

<a href="" id="event-log-processing"></a>*イベント ログの処理*  
システム イベント ログを取得して過去の WHEA ハードウェア エラーのイベント処理のクエリを実行します。

<a href="" id="event-notification"></a>*イベント通知*  
発生すると、新しいイベントを処理する WHEA ハードウェア エラーのイベントの通知を登録しています。

WHEA の管理操作には、有効化またはエラーのソースを無効にしてテスト目的でハードウェア エラーを挿入するなどのアクションが含まれます。

シングル ユーザー モード アプリケーションでは、イベントの処理および管理メカニズムの任意の組み合わせを使用できます。

WHEA ハードウェア エラーのイベント処理アプリケーションは、以降 Windows Vista でサポートされます。 WHEA のハードウェア エラーのイベントを処理するユーザー モード アプリケーションを実装する方法の詳細については、次を参照してください。 [WHEA ハードウェア エラー イベント処理アプリケーション](whea-hardware-error-event-processing-applications.md)します。

Windows Server 2008 では、WHEA 管理アプリケーションがサポートされている、Windows Vista SP1 と以降のバージョンの Windows WHEA の管理操作を実行するユーザー モード アプリケーションを実装する方法の詳細について参照[WHEA の管理アプリケーション](whea-management-applications.md)します。

 

 




