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
ms.openlocfilehash: c3559f5843513e606a591fec39a037a9d4515a5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380263"
---
# <a name="managing-memory-sections"></a>メモリ セクションの管理





ドライバーは、呼び出すことによってセクション オブジェクトを作成できます[ **ZwCreateSection**](https://msdn.microsoft.com/library/windows/hardware/ff566428)、セクション オブジェクトへのハンドルを返します。 使用して、 *FileHandle*バッキング ファイルを指定するパラメーターまたは**NULL**セクションがファイル バックアップがない場合。 使用して、セクション オブジェクトに追加のハンドルを開くことが[ **ZwOpenSection**](https://msdn.microsoft.com/library/windows/hardware/ff567029)します。

現在のプロセスのアドレス空間内でアクセス可能セクション オブジェクトに属するデータをするためには、セクションのビューを割り当てる必要があります。 ドライバーを使用して現在のプロセスのアドレス空間セクションのビューをマップすることができます、 [ **ZwMapViewOfSection** ](https://msdn.microsoft.com/library/windows/hardware/ff566481)ルーチン。 *SectionOffset*パラメーターのセクション内のビューの開始位置のバイト オフセットを指定して、 *ViewSize*マップするバイト数を指定します。

*保護*パラメーターが、ビューに対して許可された操作を指定します。 指定 ページ\_読み取り専用ビューで、ページの読み取り専用\_読み取り/書き込みのビューでは、およびページの READWRITE\_WRITECOPY するコピー オン ライト表示されます。

コンソール アプリケーションは、仮想メモリの範囲がアクセスされるまでビューの 物理メモリは割り当てられません。 メモリの範囲の最初のアクセスとページ フォールトが発生します。システムは、そのメモリ位置を保持するためにページを割り当てます。 ファイル バックアップをセクションには、システムはそのページに対応し、メモリにコピーするファイルの内容を読み取ります。 (未使用のセクション オブジェクトとビューを使用するいくつかのページおよび非ページ プールのブックキーピングのために注意してください)。

ドライバーは、ビューを使用して不要になった後、割り当てを解除を呼び出すことによって[ **ZwUnmapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff567119)します。 ドライバーがセクション オブジェクトを使用して不要になった後でセクション ハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。 ビューがマップされている他のビューがないマップすることをした後、すぐに呼び出しても安全だことに注意してください。 **ZwClose**ハンドル; 表示 (およびセクション オブジェクト) で、ビューのマップが解除されるまでに存在する続行 セクションでします。 これは、ハンドルが閉じられていないドライバーのリスクを軽減ためにの推奨される方法です。

 

 




