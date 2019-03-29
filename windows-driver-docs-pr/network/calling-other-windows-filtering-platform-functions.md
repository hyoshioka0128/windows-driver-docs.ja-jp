---
title: その他の Windows フィルター プラットフォーム関数の呼び出し
description: その他の Windows フィルター プラットフォーム関数の呼び出し
ms.assetid: dae70b4d-2be2-4db3-86cc-2e7df7d5c034
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、他の関数の呼び出し
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、その他の関数の呼び出し
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
- カーネル モード コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
- ユーザー モード コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b8ee9c6b24c69c0d8d0a43a5db24f8ac7a8f79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577893"
---
# <a name="calling-other-windows-filtering-platform-functions"></a>その他の Windows フィルター プラットフォーム関数の呼び出し


ユーザー モードの管理アプリケーションに利用できるその他の Windows フィルタ リング プラットフォーム機能の多くはコールアウト ドライバーを入手できます。 これにより、フィルター エンジンにフィルターを追加するなどの管理タスクを実行するためのコールアウト ドライバーです。 これらの関数、ユーザー モードとカーネル モードのバージョンの唯一の違いは、返されるデータ型です。 ユーザー モードの関数は、カーネル モードの関数は、同等の NTSTATUS コードを返す一方、Win32 のエラー コードを返します。

Windows フィルタ リング プラットフォームの管理機能のほとんどでは、パラメーターとして、フィルター エンジンへの開いているセッションを識別するハンドルが必要です。 次のトピックでは、コールアウト ドライバーが開くし、フィルター エンジンにセッションを閉じる方法について説明します。

[フィルター エンジンへのセッションを開く](opening-a-session-to-the-filter-engine.md)

[フィルター エンジンへのセッションを閉じる](closing-a-session-to-the-filter-engine.md)

コールアウト ドライバーから呼び出すことができる他の Windows フィルタ リング プラットフォーム関数の一覧は、次を参照してください。 [Windows フィルタ リング プラットフォーム関数のその他の](https://msdn.microsoft.com/library/windows/hardware/ff569961)します。 これらの関数を使用する方法の詳細については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK のドキュメント。

 

 





