---
title: 自動メモリ ダンプ
description: 自動メモリ ダンプ
ms.assetid: A2C71497-7865-4DC8-B760-6121B224737A
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae6b84d1c38f32e048c752f2a92d9dc1dbc31109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354408"
---
# <a name="automatic-memory-dump"></a>自動メモリ ダンプ


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*メモリ ダンプを自動*と同じ情報を含む、[カーネル メモリ ダンプ](kernel-memory-dump.md)します。 2 つの違いとは、ダンプ ファイル自体ではなくが Windows がシステムのページング ファイルのサイズを設定する方法です。

システムのページング ファイルのサイズに設定されている場合**システム管理サイズ**、カーネル モードのクラッシュ ダンプに設定されていると**メモリ ダンプを自動**Windows は RAM のサイズより小さいにページング ファイルのサイズを設定することができます。 この場合は、Windows では、ほとんどのことができます、カーネル メモリ ダンプにキャプチャされることを確認するのに十分な大きさのページング ファイルのサイズを設定します。

コンピューターがクラッシュし、ページング ファイルでないかどうか、ページングのファイルのサイズに以上で RAM のサイズが増加を Windows カーネル メモリ ダンプをキャプチャするのに十分な大きさです。 このイベントの時刻は、レジストリでは、ここに記録されます。

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**LastCrashTime**

ページング ファイル サイズの増加は、4 週間の場所にまだし、サイズを小さく絞り込みますを返します。 4 週間前に小さいページング ファイルを取得するには、レジストリ エントリを削除することができます。

ファイルの設定に移動して、ページングを表示する**コントロール パネルの &gt;システムとセキュリティ&gt;システム&gt;システムの詳細設定**します。 **[パフォーマンス]** の下にある **[設定]** をクリックします。 **詳細** タブの **仮想メモリ**、 をクリックして**変更**します。 仮想メモリ ダイアログ ボックスでは、ページング ファイルの設定を確認できます。

![仮想メモリのダイアログ ボックスのスクリーン ショット。](images/virtualmemorydialog.png)

自動メモリ ダンプ ファイルは %systemroot% に書き込まれます\\既定 Memory.dmp します。

自動メモリ ダンプは、Windows 8 以降です。

**注**  自動のメモリ ダンプをデバッグするときに、不足しているページのエラー メッセージを非表示に使用して、 [ **.ignore\_不足している\_ページ**](-ignore-missing-pages--suppress-missing-page-errors-.md)コマンド。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

[カーネル モードのダンプ ファイル](kernel-mode-dump-files.md)

[カーネル モードのダンプ ファイルを作成します。](creating-a-kernel-mode-dump-file.md)

 

 






