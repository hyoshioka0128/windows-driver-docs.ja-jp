---
title: ミニフィルター ドライバーでのコンテキストの管理
description: ミニフィルター ドライバーでのコンテキストの管理
ms.assetid: c7186886-f083-45c9-a39d-3f8ce7df35bb
keywords:
- ファイル システム ミニフィルター ドライバー WDK、コンテキスト
- ミニフィルター ドライバー WDK、コンテキスト
- コンテキスト WDK ファイル システム ミニフィルター
- WDK のコンテキストのファイル システム ミニフィルター、コンテキストについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a4381a3cc85bcb1a93c9ec9d80e1f849184fe5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571554"
---
# <a name="managing-contexts-in-a-minifilter-driver"></a>ミニフィルター ドライバーでのコンテキストの管理


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


A*コンテキスト*構造ミニフィルター ドライバーで定義されていると、フィルターのマネージャー オブジェクトに関連付けられていることができます。 ミニフィルター ドライバーは、作成し、以下のオブジェクトのコンテキストを設定できます。

-   ファイル (Windows Vista 以降のみ)。

-   インスタンス

-   Volumes

-   ストリーム

-   Stream ハンドル (オブジェクトのファイル)

-   トランザクション (Windows Vista 以降のみ)。

非ページ プールから割り当てる必要がある、ボリュームのコンテキスト以外には、コンテキストをページまたは非ページ プールから割り当てられることができます。

フィルター マネージャーに関連付けられている、オブジェクトが削除されるは、ミニフィルター ドライバーのインスタンスが、ボリュームからデタッチされている場合、またはミニフィルター ドライバーを読み込むときにコンテキストを自動的に削除します。

このセクションの内容:

[コンテキストの種類を登録します。](registering-context-types.md)

[コンテキストを作成します。](creating-contexts.md)

[コンテキストの設定](setting-contexts.md)

[コンテキストを取得します。](getting-contexts.md)

[参照元のコンテキスト](referencing-contexts.md)

[コンテキストを解放します。](releasing-contexts.md)

[コンテキストを削除します。](deleting-contexts.md)

[コンテキストを解放します。](freeing-contexts.md)

[コンテキストのファイル システムのサポート](file-system-support-for-contexts.md)

[ベスト プラクティス](best-practices.md)

 

 




