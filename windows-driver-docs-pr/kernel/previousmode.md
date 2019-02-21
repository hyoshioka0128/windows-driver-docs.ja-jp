---
title: PreviousMode
description: PreviousMode
ms.assetid: 1251cca9-604c-48c0-a136-21dd1fe4fa72
keywords:
- PreviousMode
- Requestormode で
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 968c781c98198f7be9328578b6c98adbbb1b77fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538698"
---
# <a name="previousmode"></a>PreviousMode


ユーザー モード アプリケーションを呼び出すと、 **Nt**または**Zw**サービス ルーチンのネイティブ システムのバージョン、システム コールのメカニズムは、カーネル モードへの呼び出し元のスレッドをトラップします。 システム用のトラップ ハンドラーのセットの呼び出しでパラメーター値がユーザー モードで発生したことを示す、 **PreviousMode**フィールドに、[スレッド オブジェクト](introduction-to-thread-objects.md)の呼び出し元の**UserMode**. ネイティブのシステム サービスの定期的なチェック、 **PreviousMode**ユーザー モードのソースからパラメーターかどうかを呼び出し元のスレッドのフィールド。

場合は、カーネル モード ドライバーは、ネイティブ システム サービス ルーチンとパス パラメーターがカーネル モードのソースからルーチンの値を呼び出し、ドライバーように注意してください、 **PreviousMode**に設定されている現在のスレッド オブジェクト内のフィールド**Kernelmode である**します。

カーネル モード ドライバーが任意のスレッドのコンテキストで実行できる、 **PreviousMode**にこのスレッドのフィールドを設定することがあります**UserMode**します。 このような状況で、カーネル モード ドライバーを呼び出すことができます、 **Zw**サービス パラメーターの値は、信頼できる場合は、カーネル モード ソース ルーチンを通知するルーチンのネイティブ システムのバージョン。 **Zw**をオーバーライドするシン ラッパー関数の呼び出しが、 **PreviousMode**現在のスレッド オブジェクトの値。 ラッパー関数のセット**PreviousMode**に**kernelmode である**を呼び出すと、 **Nt**ルーチンのバージョン。 戻り時にから、 **Nt**ルーチン、ラッパー関数のバージョンの復元元**PreviousMode**スレッド オブジェクトを返しますの値。

カーネル モード ドライバーを直接呼び出すことができます、 **Nt**サービス ルーチンのネイティブ システムのバージョン。 ドライバーを呼び出すことができます、カーネル モード ドライバーでは、ユーザー モードまたはカーネル モードで発生することを I/O 要求を処理するとき、 **Nt**ルーチンのバージョンを**PreviousMode**現在の値スレッドが呼び出し中に変更されません。 **Nt * Xxx*** ルーチンは、呼び出し元のスレッドを確認します**PreviousMode**パラメーターの値が、ユーザー モード アプリケーションまたはカーネル モードのコンポーネントからはと扱うかどうかを決定する値。それに応じて。

カーネル モード ドライバーを呼び出す場合、エラーが発生する可能性が、 **Nt * Xxx*** ルーチンと**PreviousMode**現在のスレッド オブジェクトの値は正確に示しませんパラメーターの値は、かどうかを。ユーザー モードまたはカーネル モードのソース。

たとえば、カーネル モード ドライバーが任意のスレッドのコンテキストで実行されていること、 **PreviousMode**値に設定されているこのスレッド**UserMode**します。 ドライバーはカーネル モード ファイル ハンドルを渡す場合、 [**そのファイルに対してクローズ**](https://msdn.microsoft.com/library/windows/hardware/ff566417)日常的なこのルーチンのチェック、 **PreviousMode**値し、ハンドルはユーザー モードである必要がありますを決定処理します。 ときに**そのファイルに対してクローズ**ハンドルが見つからないステータスを返す、ユーザー モードのハンドル テーブルで\_無効な\_ハンドル エラー コード。 一方で、ドライバーが閉じられることはカーネル モードのハンドルのリークが発生します。

別の例の場合のパラメーター、 **Nt * Xxx*** ルーチンは、入力または出力バッファーを含める場合に**PreviousMode** = **UserMode**、ルーチン呼び出し、 [ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)または[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)バッファーを検証するルーチン。 ユーザー モードのメモリ内ではなく、システム メモリ内バッファーが割り当てられている場合、 **ProbeFor * Xxx*** ルーチンは、例外が発生し、 **Nt * Xxx*** ルーチンは、状態を返します\_へのアクセス\_違反のエラー コード。

必要な場合は、ドライバーを呼び出すことができます、 [ **ExGetPreviousMode** ](https://msdn.microsoft.com/library/windows/hardware/ff545288)ルーチンを取得する、 **PreviousMode**現在のスレッド オブジェクトからの値。 または、ドライバーが読み取ることができます、 **requestormode で**フィールドを[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)要求された I/O 操作を記述する構造体。 **Requestormode で**フィールドにはコピーが含まれています、 **PreviousMode**操作を要求したスレッドからの値。

 

 




