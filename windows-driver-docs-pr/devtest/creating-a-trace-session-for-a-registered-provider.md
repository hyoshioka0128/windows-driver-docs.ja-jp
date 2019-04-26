---
title: 登録済みプロバイダーのトレース セッションの作成
description: 登録済みプロバイダーのトレース セッションの作成
ms.assetid: 3013b5fa-5390-4d46-b138-4ddcda468ddf
keywords:
- 登録されているプロバイダーの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9bd580f5251a74e34a74eee211cb3bbb3e2f9b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340612"
---
# <a name="creating-a-trace-session-for-a-registered-provider"></a>登録済みプロバイダーのトレース セッションの作成


## <span id="ddk_create_a_trace_session_for_a_registered_provider_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_FOR_A_REGISTERED_PROVIDER_TOOLS"></span>


トレース メッセージを監視する、[登録済みのプロバイダー](registered-provider.md)次の操作を行います。

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  クリックして**という名前のプロバイダー**、省略記号ボタンをクリックし、(**.**) の横にある、**という名前のプロバイダー**テキスト ボックス。

    **という名前のプロバイダーの選択**traceview でダイアログ ボックスで、システムに登録されているプロバイダーが表示されます。

5.  登録済みのプロバイダーを選択し、クリックして**OK**します。

6.  次のいずれかの操作を行います。
    -   1 つまたは複数の TMF ファイルを指定するには、次のようにクリックします。 **TMF ファイルの選択**、 をクリック**ok**、 をクリック**追加**、を参照し、ディレクトリから 1 つ以上の TMF ファイルを選択します。 別のディレクトリから TMF ファイルを選択する をクリックして、**追加**もう一度ボタンをクリックします。 それ以外の場合、をクリックして**完了**します。
    -   Traceview で指定したディレクトリ内の TMF ファイルを検索するを指示するには、次のようにクリックします。 **TMF 検索パスの設定**、 をクリック**ok**で、ディレクトリを参照し、順にクリックします**OK**。

7.  任意の型の追加のプロバイダーを追加するには、次のようにクリックします。**プロバイダーの追加**します。 この手順は省略可能です。

8.  **[次へ]** をクリックします。

9.  [基本的なトレース セッションのオプションを設定](setting-basic-trace-session-options.md)必要な場合、します。

10. [詳細トレース セッションのオプションを設定する](setting-advanced-trace-session-options.md)必要な場合、します。

11. **[Finish]**(完了) をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

TMF ファイルを指定する方法の詳細については、TMF ファイルの選択および TMF 検索パスの設定を参照してください。

登録済みのプロバイダーのフラグとレベルを設定するを参照してください。[トレース セッション オプションの高度な設定](setting-advanced-trace-session-options.md)します。

名前付きプロバイダーの一覧に表示される「Windows カーネル トレース」プロバイダーが適切と呼ばれますが、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。 使用することができます、**という名前のプロバイダーの選択**NT Kernel Logger トレース セッションを作成する ダイアログ ボックスが、このダイアログ ボックスによりトレース対象のカーネル コンポーネントを選択します。 代わりに、既定のコンポーネント (プロセス、スレッド、ディスク、およびネットワーク) を選択します。 トレース コンポーネントを選択するには、NT Kernel Logger トレース セッション用にカスタマイズされている traceview でインターフェイスを使用します。

TMF ファイルを Windows カーネル トレースで、system.tmf が WDK に含まれています。 をクリックして**TMF ファイルの選択**、 をクリックして**追加**に移動し、\\ツール\\トレース\\i386 サブディレクトリ、し system.tmf を選択します。

詳細については、次を参照してください。 [NT Kernel Logger のトレース セッションを作成する](creating-an-nt-kernel-logger-trace-session.md)します。

 

 





