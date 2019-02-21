---
title: IRP_MJ_FILE_SYSTEM_CONTROL の Oplock の状態をチェック
description: IRP_MJ_FILE_SYSTEM_CONTROL 操作の Oplock の状態を確認
ms.assetid: 3651d9ed-6b6f-4b60-9dfa-1c5c0c78b1a1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 146acf363d8c9cc363a135f88ab98efb4a69532d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531325"
---
# <a name="checking-the-oplock-state-of-irpmjfilesystemcontrol"></a>IRP_MJ_FILE_SYSTEM_CONTROL の Oplock の状態をチェック

IRP_MJ_FILE_SYSTEM_CONTROL の特定の操作では、oplock の状態を確認します。 次の処理は、このチェックを実行します。
- **FSCTL_SET_ZERO_DATA**

この情報は、呼び出し元が、指定したストリームの現在の内容は 0 たい場合に適用されます。

|要求の種類|条件|
|---|---|
|レベル 1<br>Batch (バッチ)<br>フィルター<br>読み取りハンドル<br>読み取り/書き込み<br>書き込みハンドルの読み取り|(FSCTL_SET_ZERO_DATA) をときに IRP_MJ_FILE_SYSTEM_CONTROL に分かれます。<ul><li>操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</ul></li><hr>Oplock が破損している場合。<ul><li>[なし] に中断します。</li><li>ハンドルの読み取り要求。中断の受信確認は必須ですが、すぐに (受信確認を待機することがなくなど) の操作が続行します。</li><li>他のすべての要求タイプ。操作を続行する前に、受信確認を受信する必要があります。</li></ul>|
|Read|(FSCTL_SET_ZERO_DATA) をときに IRP_MJ_FILE_SYSTEM_CONTROL に分かれます。<ul><li>操作は、oplock を所有する FILE_OBJECT から別の oplock のキーを持つ、FILE_OBJECT で発生します。</ul></li><hr>Oplock が破損している場合。<ul><li>[なし] に中断します。</li><li>受信確認は必要ありません、すぐに、操作を続行します。</li></ul>|
|レベル 2|<ul><li>[なし] に常に中断します。</li><li>受信確認は必要ありません、すぐに、操作を続行します。</li></ul>|



