---
title: メモリセクションの管理
description: メモリセクションの管理
ms.assetid: 620ba31d-596f-493a-b97f-65a27d50cc9a
keywords:
- メモリセクション WDK カーネル
- セクションオブジェクト WDK カーネル
- ビュー WDK メモリセクション
- セクションビューのマッピング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d17c553028b85c5845dfa4e028a1203b991ba77b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838545"
---
# <a name="managing-memory-sections"></a>メモリセクションの管理





ドライバーは、セクションオブジェクトへのハンドルを返す[**Zw/** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)を呼び出すことによって、セクションオブジェクトを作成できます。 *FileHandle*パラメーターを使用してバッキングファイルを指定します。または、セクションがファイルによってサポートされていない場合は**NULL**を使用します。 セクションオブジェクトへの追加ハンドルは、 [**Zwopensection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)を使用して開くことができます。

セクションオブジェクトに属するデータを現在のプロセスのアドレス空間内でアクセスできるようにするには、セクションのビューをマップする必要があります。 ドライバーは、 [**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)ルーチンを使用して、セクションのビューを現在のプロセスのアドレス空間にマップできます。 *Sectionoffset*パラメーターは、ビューがセクション内で開始する位置のバイトオフセットを指定し、 *viewsize*はマップするバイト数を指定します。

*Protect*パラメーターは、ビューで許可される操作を指定します。 読み取り専用ビューの場合は読み取り専用のページ\_を指定し、読み取り/書き込みビューの場合はページ\_読み取り/書き込みビューの場合はページ\_WRITECOPY を指定します。

仮想メモリの範囲にアクセスするまで、ビューには物理メモリが割り当てられません。 メモリ範囲の最初のアクセスでページフォールトが発生します。その後、システムはそのメモリ位置を保持するページを割り当てます。 セクションがファイルベースの場合、システムはそのページに対応するファイルの内容を読み取り、メモリにコピーします。 (未使用のセクションオブジェクトおよびビューでは、ブックキーピングのために一部のページプールと非ページプールが使用されていることに注意してください)。

ドライバーは、ビューを使用しなくなった後、 [**ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunmapviewofsection)を呼び出すことによって解除します。 ドライバーは、セクションオブジェクトを使用しなくなった後、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を使用してセクションハンドルを閉じます。 ビューがマップされ、他のビューがマップされない場合は、セクションハンドルで**Zwclose**をすぐに呼び出すことができます。ビューがマップ解除されるまで、ビュー (およびセクションオブジェクト) は引き続き存在します。 これは、ドライバーがハンドルを閉じる際のリスクを軽減するため、推奨される方法です。

 

 




