---
title: メモリ セクションの管理
description: メモリ セクションの管理
ms.assetid: 620ba31d-596f-493a-b97f-65a27d50cc9a
keywords:
- メモリのセクションでは WDK カーネル
- セクション オブジェクト WDK カーネル
- ビューの WDK メモリ セクション
- マッピングのセクションのビュー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66078fa565a02b943ff4214cc356fef276504288
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386011"
---
# <a name="managing-memory-sections"></a>メモリ セクションの管理





ドライバーは、呼び出すことによってセクション オブジェクトを作成できます[ **ZwCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection)、セクション オブジェクトへのハンドルを返します。 使用して、 *FileHandle*バッキング ファイルを指定するパラメーターまたは**NULL**セクションがファイル バックアップがない場合。 使用して、セクション オブジェクトに追加のハンドルを開くことが[ **ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)します。

現在のプロセスのアドレス空間内でアクセス可能セクション オブジェクトに属するデータをするためには、セクションのビューを割り当てる必要があります。 ドライバーを使用して現在のプロセスのアドレス空間セクションのビューをマップすることができます、 [ **ZwMapViewOfSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmapviewofsection)ルーチン。 *SectionOffset*パラメーターのセクション内のビューの開始位置のバイト オフセットを指定して、 *ViewSize*マップするバイト数を指定します。

*保護*パラメーターが、ビューに対して許可された操作を指定します。 指定 ページ\_読み取り専用ビューで、ページの読み取り専用\_読み取り/書き込みのビューでは、およびページの READWRITE\_WRITECOPY するコピー オン ライト表示されます。

コンソール アプリケーションは、仮想メモリの範囲がアクセスされるまでビューの 物理メモリは割り当てられません。 メモリの範囲の最初のアクセスとページ フォールトが発生します。システムは、そのメモリ位置を保持するためにページを割り当てます。 ファイル バックアップをセクションには、システムはそのページに対応し、メモリにコピーするファイルの内容を読み取ります。 (未使用のセクション オブジェクトとビューを使用するいくつかのページおよび非ページ プールのブックキーピングのために注意してください)。

ドライバーは、ビューを使用して不要になった後、割り当てを解除を呼び出すことによって[ **ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunmapviewofsection)します。 ドライバーがセクション オブジェクトを使用して不要になった後でセクション ハンドルを閉じる[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 ビューがマップされている他のビューがないマップすることをした後、すぐに呼び出しても安全だことに注意してください。 **ZwClose**ハンドル; 表示 (およびセクション オブジェクト) で、ビューのマップが解除されるまでに存在する続行 セクションでします。 これは、ハンドルが閉じられていないドライバーのリスクを軽減ためにの推奨される方法です。

 

 




